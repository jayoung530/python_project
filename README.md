# 전국 고속도로 휴게소 지도

학과 | 학번 | 성명
---- | ---- | ---- 
독어독문학과 |201502228 |홍자영


## 프로젝트 개요
한국 도로공사의 전국 휴게소 정보 csv파일을 읽어와서 국내 고속도로 휴게소의 위치를 보기쉽게 지도에 표시하였습니다.
또한 휴게소 종류별로 색을 다르게 하여 보기 쉽도록 했으며, 아이콘에 휴게소의 명칭을 명시하여 이름정보를 알 수 있도록 하였습니다.

## 사용한 공공데이터 
[데이터보기](https://github.com/jayoung530/python_project/blob/master/%ED%95%9C%EA%B5%AD%EB%8F%84%EB%A1%9C%EA%B3%B5%EC%82%AC_%ED%9C%B4%EA%B2%8C%EC%86%8C%EC%A0%95%EB%B3%B4_20171114.csv)

## 소스
* [링크로 소스 내용 보기](https://github.com/jayoung530/python_project/blob/master/201502228) 

~~~python

import pandas as pd
import folium
import warnings

warnings.filterwarnings('ignore')

target_csv = '한국도로공사_휴게소정보_20171114.csv'

total = pd.read_csv(target_csv, encoding='euc-kr')
df_pos = total[['위도','경도','휴게소명','휴게소종류']]
print(df_pos)
map = folium.Map(location=[df_pos['위도'].mean(), df_pos['경도'].mean()], zoom_start=8)
iconcolour=''
for n in df_pos.index:
    popup_name = df_pos['휴게소명'][n]
    if df_pos['휴게소종류'][n]=='일반휴게소':
        iconcolour='red'
    elif df_pos['휴게소종류'][n]=='간이휴게소':
        iconcolour='blue'
    else:
        iconcolour='green'


    folium.Marker([df_pos['위도'][n], df_pos['경도'][n]],
                  popup=popup_name,
                  icon=folium.Icon(color=iconcolour)).add_to(map)



map.save('C:/Users/SAMSUNG/Desktop/map1.html')
~~~
![screenshot](https://github.com/jayoung530/python_project/blob/master/%EA%B3%A0%EC%86%8D%EB%8F%84%EB%A1%9C%EC%A7%80%EB%8F%84.png)
![screenshot1](https://github.com/jayoung530/python_project/blob/master/%EA%B3%A0%EC%86%8D%EB%8F%84%EB%A1%9C%EC%A7%80%EB%8F%84_%EC%9D%B4%EB%A6%84%ED%91%9C%EC%8B%9C.png)
