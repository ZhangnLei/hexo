---
title: 后端开发 - Java反射获取类的所有的属性和父类的所有属性
date: 2020-07-16 10:05:26
tags:
- 反射
- 获取父类的所有属性
---

[toc]

## 问题

想获取一个类的所有属性和父类的所有属性

看一下官方文档中关于获取类的属性的两个方法：

1. ### getDeclaredFields

返回一个字段对象数组，反映由这个类对象表示的类或接口声明的所有字段。这包括公共、受保护、默认(包)访问和私有字段，但不包括继承字段。

2. ### getFields

返回一个包含“字段”对象的数组，该数组反映由这个“类”对象表示的类或接口的所有可访问的公共字段。



这两个方法都不能获取所有属性，那我们自己写一个方法。

## 思路

首先构建一个列表用来存放所有的属性；

获取使用getDeclaredFields()函数获取本类内部的所有属性，并addAll()到列表中；

使用clazz.getSuperclass()方法获取父类，然后获取父类中的所有属性，将其添加到列表中；

最后递归检查父类是否有父类，直到获取不到父类；

## 编码

```java
	/**
	 * 获取本类及其父类的属性的方法
	 * @param clazz 当前类对象
	 * @return 字段数组
	 */
	private static Field[] getAllFields(Class<?> clazz) {
		List<Field> fieldList = new ArrayList<>();
		while (clazz != null){
			fieldList.addAll(new ArrayList<>(Arrays.asList(clazz.getDeclaredFields())));
			clazz = clazz.getSuperclass();
		}
		Field[] fields = new Field[fieldList.size()];
		return fieldList.toArray(fields);
	}

	public static void main(String[] args) {
		Field[] clzFields = getAllFields(AppSysUnitVo.class);
		for (Field clzField : clzFields) {
			try {
				if (!clzField.isAccessible()) {
					clzField.setAccessible(true);
				}
				System.out.println(clzField.getName());
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	}
```



更多详细代码见我的代码仓库

[https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/sy](https://github.com/ZhangnLei/java-base/tree/master/src/main/java/mrzhang/sy)





## 官方文档：

### getDeclaredFields

> ```
> public Field[] getDeclaredFields()
>                           throws SecurityException
> ```
>
> Returns an array of `Field` objects reflecting all the fields declared by the class or interface represented by this `Class` object. This includes public, protected, default (package) access, and private fields, but excludes inherited fields.
>
> If this `Class` object represents a class or interface with no declared fields, then this method returns an array of length 0.
>
> If this `Class` object represents an array type, a primitive type, or void, then this method returns an array of length 0.
>
> The elements in the returned array are not sorted and are not in any particular order.
>
> - **Returns:**
>
>   the array of `Field` objects representing all the declared fields of this class
>
> - **Throws:**
>
>   `SecurityException` - If a security manager, *s*, is present and any of the following conditions is met:the caller's class loader is not the same as the class loader of this class and invocation of [`s.checkPermission`](dfile:///Users/zhangdabao/Library/Application Support/Dash/DocSets/Java_SE8/Java.docset/Contents/Resources/Documents/java/lang/SecurityManager.html#checkPermission-java.security.Permission-) method with`RuntimePermission("accessDeclaredMembers")` denies access to the declared fields within this classthe caller's class loader is not the same as or an ancestor of the class loader for the current class and invocation of [`s.checkPackageAccess()`](dfile:///Users/zhangdabao/Library/Application Support/Dash/DocSets/Java_SE8/Java.docset/Contents/Resources/Documents/java/lang/SecurityManager.html#checkPackageAccess-java.lang.String-) denies access to the package of this class
>
> - **Since:**
>
>   JDK1.1
>
> - **See The Java™ Language Specification:**
>
>   8.2 Class Members, 8.3 Field Declarations

### getFields

> ```
> public Field[] getFields()
>                   throws SecurityException
> ```
>
> Returns an array containing `Field` objects reflecting all the accessible public fields of the class or interface represented by this `Class` object.
>
> If this `Class` object represents a class or interface with no no accessible public fields, then this method returns an array of length 0.
>
> If this `Class` object represents a class, then this method returns the public fields of the class and of all its superclasses.
>
> If this `Class` object represents an interface, then this method returns the fields of the interface and of all its superinterfaces.
>
> If this `Class` object represents an array type, a primitive type, or void, then this method returns an array of length 0.
>
> The elements in the returned array are not sorted and are not in any particular order.
>
> - **Returns:**
>
>   the array of `Field` objects representing the public fields
>
> - **Throws:**
>
>   `SecurityException` - If a security manager, *s*, is present and the caller's class loader is not the same as or an ancestor of the class loader for the current class and invocation of [`s.checkPackageAccess()`](dfile:///Users/zhangdabao/Library/Application Support/Dash/DocSets/Java_SE8/Java.docset/Contents/Resources/Documents/java/lang/SecurityManager.html#checkPackageAccess-java.lang.String-) denies access to the package of this class.
>
> - **Since:**
>
>   JDK1.1
>
> - **See The Java™ Language Specification:**
>
>   8.2 Class Members, 8.3 Field Declarations

