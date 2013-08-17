//.h
static vector<string> split(string str,string pattern);//字符串分割
static bool isContantString(string sourceStr,string patternStr);//判断一个字符串是否包含另外一个

static vector<vector<string> > paserExcel(string detailStr);

//.M部分
//c++字符串分割函数
vector<string>PersonalApiCplu::split(string str,string pattern)
{
    std::string::size_type pos;
    std::vector<std::string> result;
    str+=pattern;//扩展字符串以方便操作
    int size=str.size();
    
    for(int i=0; i<size; i++)
    {
        pos=str.find(pattern,i);
        if(pos<size)
        {
            std::string s=str.substr(i,pos-i);
            result.push_back(s);
            i=pos+pattern.size()-1;
        }
    }
    return result;
}


bool PersonalApiCplu::isContantString(string sourceStr,string patternStr)
{
    const char *show;
    
    show=strstr(sourceStr.c_str(),patternStr.c_str());//返回指向第一次出现r位置的指针，如果没找到则返回NULL。
    
    bool isContant;
    if (show == NULL)
    {
        isContant = NO;
    }
    else
    {
        isContant = YES;
    }
    
    return isContant;
}

vector<vector<string> > ExcelParser::paserExcel(string detailStr)
{
    vector<vector<string> > ivec;
    //去头莫名奇妙都会多出第一行为空，内容都从数组的第二位开始
    //去尾莫名其妙多最后一位。
    string pattern1("<Row ss:AutoFitHeight=\"0\">");//去头
    
    vector<string>ivec1 =  PersonalApiCplu::split(detailStr,pattern1);//取出所有单词套组
    
    for (int j = 1;j<ivec1.size(); j++)
    {
        if (j == 59)
        {
            ;
        }
        vector<string> tempIvec;
        
        string pattern2("</Data></Cell>");//去尾
        vector<string>ivec2 =  PersonalApiCplu::split(ivec1[j],pattern2);//某个单词组中的所有元素
       
        
        for (int i = 0;i<ivec2.size()-1; i++)//去尾
        {
            string sourceStr = ivec2[i];
            
            string patternStr = "</Font>";
            
            
            if (PersonalApiCplu::isContantString(sourceStr,patternStr))//判断是否可以直接取，或者是要通过字符串合并
            {
                string pattern3("</Font>");//去尾
                vector<string>ivec3 =  PersonalApiCplu::split(ivec2[i],pattern3);
                
                
                string s4;
                string pattern4("xmlns=\"http://www.w3.org/TR/REC-html40\">");//去头
                for (int k = 0; k<ivec3.size()-1; k++)//记得减去数组最后一位，去尾莫名其妙多最后一位。
                {
                    vector<string>ivec4 =  PersonalApiCplu::split(ivec3[k],pattern4);
                    s4 += ivec4[1];
                }
                
                tempIvec.push_back(s4.c_str());
            }
            else
            {
               
                string pattern3("<Data ss:Type=\"String\">");
                vector<string>ivec3 =  PersonalApiCplu::split(ivec2[i],pattern3);
                string s3 =  ivec3[1];
                
                tempIvec.push_back(s3.c_str());
            }
        }
        
        ivec.push_back(tempIvec);
    }
    return ivec;

}
