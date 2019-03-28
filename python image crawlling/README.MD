# 파이썬 이미지 크롤링 (무신사)

***

## 1. 폴더에 연습해볼 파일(.py)을 생성하고 코드를 긁어온다.


![코드 긁어오기](https://user-images.githubusercontent.com/38044331/55089058-2aaf1080-50f0-11e9-91ff-5105f73caa6f.PNG)  
#


### 2. 라이브러리 설치


![requests](https://user-images.githubusercontent.com/38044331/55089091-369ad280-50f0-11e9-8c4f-02218505be30.PNG)


![selenium](https://user-images.githubusercontent.com/38044331/55089113-3ef30d80-50f0-11e9-9ef2-7c70a0240771.PNG)


![numpy](https://user-images.githubusercontent.com/38044331/55089129-44e8ee80-50f0-11e9-995a-e081edd0344f.PNG)


![bs4](https://user-images.githubusercontent.com/38044331/55089153-529e7400-50f0-11e9-913b-6190a5839106.PNG)


![beautifulsoup4](https://user-images.githubusercontent.com/38044331/55089166-57632800-50f0-11e9-97f9-0e8ea48d206d.PNG)  
#


### 3. 웹드라이버 경로 설정하기


![follow2](https://user-images.githubusercontent.com/38044331/55089185-5c27dc00-50f0-11e9-9d2e-857a51f0ca3a.PNG)  
#

- **웹드라이버의 경로는 자신이 설치한 chromedriver가 있는 폴더로 들어간 후에**

![follow6](https://user-images.githubusercontent.com/38044331/55092230-89c35400-50f5-11e9-9325-10200918448e.PNG)  
#

- **클릭후에 ctrl + c 로 경로를 복사해서 넣어준 후에 /chromedriver.exe까지 넣어준다.**

![follow7](https://user-images.githubusercontent.com/38044331/55092234-8c25ae00-50f5-11e9-8d87-807d9aa4fbc2.PNG)  
#


### 4. 파이썬 파일(.py)가 있는 폴더에 'top', 'outer', 'bottom' 폴더 만들어주기


![follow3](https://user-images.githubusercontent.com/38044331/55089198-62b65380-50f0-11e9-8d38-2aac382f32c4.PNG)


### 5. 실행(자신의 파일명으로)!


![follow4](https://user-images.githubusercontent.com/38044331/55089217-68139e00-50f0-11e9-97fa-2b1475fad922.PNG)  
#

- **실행을 하거나 라이브러리를 설치할때는 항상 파일이 있는 폴더로 이동해서 진행해야한다.**
    - 현재 내 파일이 있는 폴더의 위치이다.
    
![follow8](https://user-images.githubusercontent.com/38044331/55092236-8d56db00-50f5-11e9-8785-520c43dffea4.PNG)

    - 그림에서 보는것 처럼 ls를 이용해서 파일 리스트들을 볼 수 있고, cd를 이용해서 접근이 가능하다.
    
![follow9](https://user-images.githubusercontent.com/38044331/55092238-8e880800-50f5-11e9-8ccd-eb4ef59b8aaa.PNG)

    - cd를 이용해서 한번에 접근도 가능하다.
    
![follow10](https://user-images.githubusercontent.com/38044331/55092248-921b8f00-50f5-11e9-8223-e1bc0fe7d7f8.PNG)  
#

### 실행결과 이미지가 크롤링 된것을 확인할 수 있다.


![follow5](https://user-images.githubusercontent.com/38044331/55089230-6f3aac00-50f0-11e9-9b0c-437bd2d34dbf.PNG)

***

```python
import urllib.request
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 
import time,csv
from selenium.webdriver.support.ui import WebDriverWait
import numpy
chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument("--incognito")
browser = webdriver.Chrome('C:/Users/Yechan//Desktop/chromedriver_win32/chromedriver.exe')
# 지정해준 url을 가져올때 각 HTML요소가 나타날 때 까지 최대 1.5초까지'관용있게' 기다려준다. 
browser.implicitly_wait(1.5)

# 원하는 카테고리 설정
cat=['top','outer','bottom']
#  카테고리에 해당하는 무신사 url
num=['001','002','003']

def download_img(img,category,cnt,ext):
    path = './'+category+'/'+cnt+'.'+str(ext)
    # urlretrieve: url에서 파일을 저장하기 위해서 사용하는 urllib의 매서드
    # urllib.request.urlretrieve(image_url, 로컬에 저장할 위치)
    urllib.request.urlretrieve(img,path)

# 무신사 사이트에 들어가면 페이지 전체를 로딩하기 위해서는 시간이 걸리기에 pause_time을 설정해준다.
# 또한 scroll action을 할때도, 거기에 따라서 load를 받아야 하니 pause time을 넣어준다.
SCROLL_PAUSE_TIME=0.1  
url = 'https://store.musinsa.com/app/items/lists/'

for c,j in zip(cat,num):
    # 원하는 카테고리로 url을 쏴준다
    browser.get(url+j)
    # 셀레늄 window를 최대화 시켜서 킨다.
    browser.maximize_window()
    # 현재 저장하는 파일이 몇번째 인지 가지고 있는 변수( 파일이름 중첩 방지, ex_ 001.png 002.png )
    # 참고로 페이지를 돌면서 idx가 0으로 초기화되기때문에 cur_num변수가 필요하다.
    cur_num = 0
        
    #  만약 사진 외에도 가격 브랜드 등을 가져오고 싶으면 주석 풀면 됨
    #  save to csv
    title_li=[]
    price_li=[]
    like_li=[]
    ids = []
    #  무신사는 제품들이 page화 되어 있기에 어디어디 페이지를 가져올지 지정
    # range(4,5) = 4번째 page한개만 크롤링하겠다는 뜻.(원한다면 수정 가능)
    for page in range(4,5):
        # 화면 이동 사이즈 (스크롤)
        target = 1000;
        # 스크롤 pause
        time.sleep(3)
        # window의 맨 밑으로 scroll 되기 전까지 target을 이동시킨다.
        while True:
            now_height = browser.execute_script("return window.pageYOffset;")
            browser.execute_script("window.scrollTo(0,{});".format(target))
            time.sleep(SCROLL_PAUSE_TIME)
            target+=1000
            new_height = browser.execute_script("return window.pageYOffset;")
            # 현재 위치가 더이상 갈곳이 없다면 값이 같게 되며, break 처리된다.
            if now_height==new_height:break
        # 스크롤을 완료하면 모든 제품들이 load되는데, items로 가져온다.
        items = browser.find_element_by_id('searchList')
        # items에서 images tag를 가져온다
        images = items.find_elements_by_css_selector('div.li_inner > div.list_img > a > img[src]')
        # images tag 정보중 src를 가져온다.
        image_urls=[]
        
        for image in images:
            # images tag 정보중 src를 가져온다.
            image_urls.append(image.get_attribute("src"))
        # 만약 csv로 따로 저장하지 않으려면, cnt_브랜드명_가격.jpg 이런식으로 img를 저장시킨다.
        for idx,image_url in enumerate(image_urls):
            ext = image_url.split('.')[-1]
            if ext in ['jpg','png','jpeg','JPG','JPEG','PNG']:
                # 제품이있는 index를 str(idx+1) 로 전달하면 for문을 돌면서 차례차례로 아이템들이 추출된다.
                item = items.find_element_by_css_selector('#searchList > li:nth-child('+str(idx+1)+') > div.li_inner > div.article_info')
                # 그 중에서도 a tag에존재하는 title(제품명)을 긇어온다.
                title = item.find_element_by_css_selector('p.item_title > a')
                try:
                    # price 추출
                    price = item.find_element_by_class_name('price')
                    price=price.text.split()[-1][:-1].replace(',','')
                except:
                    # 만약 price가 공란일 경우에는 0값으로 에러처리
                    price = '0'
                try:
                    like = item.find_element_by_class_name('txt_cnt_like')
                    # 좋아요 수를 크롤링한다.
                    # 좋아요 같은 경우에는 1,000 따위의 형식은 int(1,000)이 파이썬에서 불가능하기때문에, int(1000)으로 수정해주어야 한다.
                    # replace를 사용하여 ,를 지워준다.('')
                    like = like.text.replace(',','')
                except:
                    # 만약 like가 공란일 경우에는 0값으로 에러처리
                    like = '0'
                title=title.text
                #  save to csv
                #  download_img(image_url,c,cur_num+idx,ext)
                # csv로 저장하지 않는다면, 데이터용량을줄이기 위하여 이미지 파일이름에 기타 정보값들을 넣어준다.
                file_name=str(cur_num+idx)+'_'+title+'_'+price+'_'+like
                title_li.append(title)
                price_li.append(price)
                like_li.append(like)
                ids.append(cur_num+idx)
                download_img(image_url,c,file_name,ext)  
            else:
                print("error made")
        # 현재까지 저장된 아이템의 갯수를 넣어준다.(for문을 돌면서 페이지가 전환될때 idx값이 0으로 초기화되기때문에)
        cur_num+=len(image_urls)
        # 다음(페이지)로 가는 버튼을 찾는다.
        button = browser.find_element_by_xpath('//*[@id="contentsItem_list"]/div[2]/div[5]/div/div/a['+str(page)+']')
        # 다음(페이지)으로 가기 버튼 클릭
        button.send_keys(Keys.ENTER)


    #  save to csv
    # tmp = numpy.asarray([*zip(ids,title_li,price_li,like_li)])
    # 파일을 열어서 저장시키기 위해서는 with구문을 사용한다.
    # csv형식으로 'w' = write
    # utf-16은 한글인코딩 깨짐 방지
    with open('./'+c+'/'+c+'.csv', 'w', encoding='utf-16') as file:
        writer = csv.writer(file, delimiter=',')
        # writer.writerow(fieldnames)
        for i,t,p,l in zip(ids,title_li,price_li,like_li):
           writer.writerow([i,t,p,l])
