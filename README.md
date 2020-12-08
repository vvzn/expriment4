# expriment4
## 一、阅读程序（代码）
``` 
package fourthText;
import java.io.*;
import java.util.Scanner;
public class FileInAndOut {
	int n;
	public String operationFile(String longer) {
		String l=null;
		String s;
	    char[] a;
		for(int i = 0;i<longer.length();i=i+7) {
			 a=new char[7];
			 try {
				 longer.getChars(i, i+7, a, 0);
		       } catch( Exception ex) {
		            System.out.println("触发异常...");
		        }
			s = String.valueOf(a);
			if(l==null) {
				l=s;
				}
			else if(l!=null)
				l=l+s;
			if(((i+7)/7)%2==1) {
				l=l+",";
				}
			else if(((i+7)/7)%2==0) {
                l=l+"。\n";
			}
		}
		return l;
	}
	public String readFile() {
		String original = null;
		int n=-1;
		char[] a = new char[100];//缓存，
		try {
			File file = new File("e:\\B.txt");
			InputStream fli = new FileInputStream(file);
			InputStreamReader in = new InputStreamReader(fli, "GBK");
		while((n=in.read(a,0,100))!=-1) {
		String s = new String(a,0,n);
		this.n=n;
		if(original!=null)
		original = original+s;
		else original=s;
		}
        in.close();
      	}
		catch (IOException e) {
			System.out.println("File read erroe:"+e);
		}
		return original;
	}
	public boolean outFile(String a) {
		byte [] b = a.getBytes();
		try {
			File file = new File("e:\\A.txt");
			OutputStream out = new FileOutputStream(file,true);
            out.write(b);
            out.flush();
            out.close();
		}
		catch (IOException e) {
			System.out.println("File read erroe:"+e);
		}
		 return true;
		}
}

package fourthText;
public class JudgeException extends Exception{
	String message;
	public String JudgeException(String input) {
		message = "您输入的“"+input+"”不正确，请输入正确性别！";
		return message;
	}
	public String JudgeException(int input) {
		message = "您输入的“"+input+"”不正确，请输入正确年龄！";
		return message;
	}
}

package fourthText;
import java.util.Scanner;
public class Student {
	String name;
	String sex;
	int age;
	String stuNo;
public void inputInformation() {
	Scanner reader = new Scanner(System.in);
	a:for(;;) {
		try {
			System.out.println("请输入姓名");
	        name=reader.nextLine();
	        System.out.println("录入成功~");
	        break a;
		}
		catch(Exception e) {
			System.out.println("您输入的 “"+name+"” 格式不正确，请重新输入！");
		}
	}
	b:for(;;) {
	try{
	System.out.println("请输入性别（中文）");
	sex=reader.nextLine();
	sexJudge(sex);
	break b;
	}
	catch(JudgeException e) {
		System.out.println(e.JudgeException(sex));
	}
	}
	c:for(;;) {
		try{
			System.out.println("请输入年龄（15-75岁）");
			age=reader.nextInt();
		    ageJudge(age);
		    break c;
		}
		catch(JudgeException e) {
			System.out.println(e.JudgeException(age));
		}
		}
	d:for(;;) {
		try {
			Scanner reader0 = new Scanner(System.in);
			System.out.println("请输入学号");
			stuNo=reader0.nextLine();
	        System.out.println("录入成功~");
	        break d;
		}
		catch(Exception e) {
			System.out.println("您输入的“"+stuNo+"”格式不正确，请重新输入！");
		}
	}
}
public void sexJudge(String sex) throws JudgeException{
	String x="男";
	String y="女";
	if (sex.equals(x)||sex.equals(y)){
		System.out.println("录入成功~");
		}
	else throw new JudgeException();
}
public void ageJudge(int age) throws JudgeException{
	int x=15;
	int y=75;
	if (age>=x&&age<=y){
		System.out.println("录入成功~");
		}
	else throw new JudgeException();
}
}

package fourthText;
public class Test {
	static Student student0=new Student();
	//static Student student1=new Student(student0.name,student0.sex,student0.age,student0.stuNo);
	static FileInAndOut file = new FileInAndOut();
	public static void main(String[] args) {
		
		  System.out.println("第四次实验：文件操作");
		  System.out.println("**********学生信息录入**********");
		  student0.inputInformation(); 
		  System.out.println("\n\n个人信息：");
		  System.out.println("姓名 性别 年龄 学号");
    	  System.out.println(student0.name+"   "+student0.sex+"    "+student0.age+"    "+student0.stuNo);
		String a=file.readFile();
		String b = file.operationFile(a);
		if(file.outFile(addNewInformation(student0)))
		System.out.println("信息导入成功！");
		if(file.outFile(b))
			System.out.println("作业导入成功！");
	}
	public static String addNewInformation(Student student) {
		String information = null;
		information="个人信息：\n姓名 性别 年龄 学号\n"+student0.name+"  "+student0.sex+"  "+student0.age+"  "+student0.stuNo+"\n完成作业：\n";
		 return information;
	}
}
``` 

## 二、实验要求
<br>1、在某课上,学生要提交实验结果，该结果存储在一个文本文件A中。
<br>2、文件A包括两部分内容：一是学生的基本信息；二是学生处理后的作业信息，该作业的业务逻辑内容是：
<br>3、利用已学的字符串处理知识编程完成《长恨歌》古诗的整理对齐工作，写出功能方法，
<br>4、实现如下功能：
<br>1）每7个汉字加入一个标点符号，奇数时加“，”，偶数时加“。”
<br>2）允许提供输入参数，统计古诗中某个字或词出现的次数
<br>3）输入的文本来源于文本文件B读取，把处理好的结果写入到文本文件A
<br>4）考虑操作中可能出现的异常，在程序中设计异常处理程序

## 三、实验目的
<br>1、掌握字符串String及其方法的使用;
<br>2、掌握文件的读取/写入方法;
<br>3、掌握异常处理结构。

## 四、实验过程
<br>1、把长恨歌的内容写在一个txt文本里面,然后用类似输入流的方法让程序读取文本文字,从而实现将长恨歌以正确的古诗文形式存储到新的txt文件中。
<br>2、在Student里面定义学生的姓名，性别，年龄，学号，用异常处理来处理那些输入格式不正确的文字。

## 五、核心方法
<br>1、如何做到把长恨歌存储到txt文本并以正确格式输出：
``` 
public String readFile() {
  String original = null;
  int n=-1;
  char[] a = new char[100];//缓存，
  try {
   File file = new File("e:\\B.txt");
   InputStream fli = new FileInputStream(file);
   InputStreamReader in = new InputStreamReader(fli, "GBK");
  while((n=in.read(a,0,100))!=-1) {
  String s = new String(a,0,n);
  this.n=n;
  if(original!=null)
  original = original+s;
  else original=s;
  }
  
        in.close();
       }
  catch (IOException e) {
   System.out.println("File read erroe:"+e);
  }
  return original;
 }
```
<br>2、如何把学生信息录入到新的txt文件里面（以姓名为例）：
```
public void inputInformation() {
 Scanner reader = new Scanner(System.in);
 a:for(;;) {
  try {
   System.out.println("请输入姓名");
         name=reader.nextLine();
         System.out.println("录入成功~");
         break a;
  }
  catch(Exception e) {
   System.out.println("您输入的 “"+name+"” 格式不正确，请重新输入！");
  }
 }
```
## 六、实验结果
<br>个人信息：
<br>姓名 性别 年龄 学号
<br>王梓楠   女    19    2019310173
<br>信息导入成功！
<br>作业导入成功！

## 七、实验感想
这次实验比上次简单一点，对于编写程序有了更深层次的理解，把书大概读了读，终于对java编程入了门，主要是在异常处理这块还不是很熟悉。
