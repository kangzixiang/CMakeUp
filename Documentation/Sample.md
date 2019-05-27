# Sample
#include "Markup.h"
#include <iostream>
#include <iomanip>
#include <map>
using namespace std;

typedef map<CString,CString> ccmap;
//写函数
bool WriteFunc(ccmap status)
{
    CMarkup xml_CMarkup;//声明xml cmark对象
    xml_CMarkup.AddElem("ROOT");
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("HEAD");
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("x0",status["01"]);
    xml_CMarkup.AddElem("x1",status["02"]);
    xml_CMarkup.OutOfElem();
    xml_CMarkup.AddElem("BODY");
    xml_CMarkup.SetAttrib("id","C");//设置某一具体属性的值,可以是数字，可以是字符
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("st","0");
    xml_CMarkup.AddElem("mi");
    xml_CMarkup.SetAttrib("style",1);//设置某一具体属性的值,可以是数字，可以是字符
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("qs","01");
    xml_CMarkup.AddElem("cs","02");
    xml_CMarkup.AddElem("rs","03");
    xml_CMarkup.AddElem("dk","04");
    xml_CMarkup.AddElem("ls","05");
    xml_CMarkup.AddElem("pt","06");
    xml_CMarkup.AddElem("fj","07");//增加元素
    xml_CMarkup.OutOfElem();
    xml_CMarkup.OutOfElem();//退出当前元素
    CString xml_out_doc= xml_CMarkup.GetDoc();//将xml转换为字符串
    std::cout<<xml_out_doc<<std::endl;
    xml_CMarkup.Save("Sample.xml");//将文件保存为xml

    return true;
}
//读函数
bool ReadFunction(ccmap &status)
{
    CMarkup xml_CMarkup;//声明xml cmark对象
    xml_CMarkup.Load("Sample.xml");//从一个文件读取xml内容
    //CString xml_Doc;
    //xml_CMarkup.SetDoc(xml_Doc);//从字符串中导入xml数据
    xml_CMarkup.FindElem();//找到第一个节点，即根节点
    //cout<<xml_CMarkup.GetTagName();//获取标签名称

    xml_CMarkup.IntoElem();//进入到这个节点
    xml_CMarkup.FindElem("HEAD");
    xml_CMarkup.IntoElem();
    xml_CMarkup.FindElem("x0");
    MCD_STR strSN1 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_head_x0",strSN1));
    xml_CMarkup.FindElem("x1");
    MCD_STR strSN2 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_head_x1",strSN2));
    xml_CMarkup.OutOfElem();
    xml_CMarkup.FindElem("BODY");
    //cout<<xml_CMarkup.GetAttribName(0)<<endl;获取属性名称，0，代表第一个，1代表第二个。。。
    MCD_STR strSN3=xml_CMarkup.GetAttrib("id");//获取属性值
    status.insert(pair<CString,CString>("a_body_zhunn",strSN3));
    xml_CMarkup.IntoElem();
    xml_CMarkup.FindElem("st");
    MCD_STR strSN4 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_body_st",strSN4));
    xml_CMarkup.FindElem("mi");
    MCD_STR strSN5=xml_CMarkup.GetAttrib("style");//获取属性值
    status.insert(pair<CString,CString>("a_body_mi",strSN5));
    xml_CMarkup.IntoElem();
    xml_CMarkup.FindElem("qs");
    MCD_STR strSN6 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_qs",strSN6));
    xml_CMarkup.ResetMainPos();//如果无法确定姊妹元素的顺序，在两次调用FindElem方法之间使用，使指向父节点
    xml_CMarkup.FindElem("cs");
    MCD_STR strSN7 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_cs",strSN7));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("rs");
    MCD_STR strSN8 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_rs",strSN8));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("dk");
    MCD_STR strSN9 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_dk",strSN9));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("ls");
    MCD_STR strSN10 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_ls",strSN10));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("pt");
    MCD_STR strSN11 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_pt",strSN11));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("fj");
    MCD_STR strSN12 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_fj",strSN12));
    status.insert(pair<CString,CString>("test","test"));
    return true;
}

//主函数

int main()
{ 
    ccmap writeMap;
    ccmap readMap;
    ccmap::iterator iter;
    writeMap.insert(pair<CString,CString>("01","0312"));
    writeMap.insert(pair<CString,CString>("02","9999999"));
    WriteFunc(writeMap);
    ReadFunction(readMap);
    for (iter=readMap.begin();iter!=readMap.end();iter++)
    {
        cout<<setw(10)<<iter->first<<"  :   "<<iter->second<<endl;
    }
    system("pause");
    return 0;
}