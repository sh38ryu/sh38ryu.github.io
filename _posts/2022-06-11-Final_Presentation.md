---
title:  "Linear Algebra - Final Presentation"
excerpt: "final presentation 2022-06-13"

toc_label: "CONTENTS"
categories:
  - LinearAlgebra
tags:
  - LinearAlgebra
last_modified_at: 2022-06-11T11:33:00-05:00
---

# Final Presentation

Parcel delivery system using rechargeable drone based on an uncertain public transportation network

# Contents

> 1. Introduction
> 2. Literature Review
> 3. Methodology
> 4. Data
> 5. Experimental Results
> 6. Conclusion




# 1. Introduction

## A) Background

**Minimizing delivery time & express delivery has become a crucial issue**

![Fast Delivery.png](/assets/images/posts/2022-06-11/1-A_FastDelivery.png){: width="500" height="100"}{: .align-center}
* Same-day delivery
* Early morning delivery
* Rocket delivery
* . . .

The demand for speed has outstripped the capabilities of railroads, trucks, ships, and planes

> **Drone Delivery** : A Solution to Last Mile Delivery!

**Current situations of drone delivery**

![Truck and Drone Delivery.png](/assets/images/posts/2022-06-11/1-A_DroneDelivery.png){: width="600" height="350"}{: .align-center}

* **Walmart**
  * expands drone delivery network providing the potential to reach 4 million U.S. households across six states (Arizona, Arkansas, Florida, Texas, Utah and Virginia) by the end of this year

* **Wing**
  * Delivering daily necessities over small and medium-sized cities in the United States, Australia, and Finland
  * 100,000 drone deliveries (2021.08)

![Truck and Drone Delivery.png](/assets/images/posts/2022-06-11/1-A_DD.png){: width="600" height="350"}{: .align-center}

* **Several drone delivery tests in Korea**
  * Domino Pizza Delivery at Sejong Lake Park
  * Delivery of masks in Jeju and Marado Island

* **etc**
  * COVID-19 diagnostic kit, medicine, food, deliver blood in Rwanda

**Cooperative Drone Delivery with Public Transportation**

The pros and cons of different types of delivery systems

![Public Transit and Drone Delivery.png](/assets/images/posts/2022-06-11/1-A_PsNg.png){: width="700" height="300"}{: .align-center}

## B) Purpose of Research
* Establish a delivery system combining drone and public transportation
* Improve delivery efficiency by introducing drone battery charging system
* Improve the applicability of this system by considering the uncertainty of link travel time of public transportation



# 2. Literature Review


## A) Drone & Public Transportation Delivery
![Literature Review - summary.png](/assets/images/posts/2022-06-11/2-A-1_LiteratureReview.png){: width="900" height="150"}{: .align-center}


## B) Link Travel Time of Public Transportation

**Rahman et al. (2018). Analysis of bus travel time distributions for varying horizons and real-time applications**

* *pseudo horizon* : the distance from a GPS point to an upstream GPS point
![Pseudo Horizon.png](/assets/images/posts/2022-06-11/2-B-1_PseudoHorizon.png){: width="500" height="150"}{: .align-center}
* analyze the changes of bus travel time characteristics as pseudo horizon varies and how such characteristics can be applied to real-time bus arrival estimation
* Instead of ~~point estimates~~ of bus arrival times, his study provides **interval estimates** that take into account the uncertainty of future bus arrival times
* Show a significant change in bus travel time characteristics around a pseudo horizon range of 8 km
![Rank of Distributions.png](/assets/images/posts/2022-06-11/2-B-2_RankOfDistribution.png){: width="500" height="600"}{: .align-center}



# 3. Methodology


## A) Choudhury et al. (2019)

**Dynamic real-time multimodal routing with hierarchical hybrid planning**

![DreamrHHP.png](/assets/images/posts/2022-06-11/3-A-1_DreamrHHP.png){: width="250" height="250"}{: .align-center}

Based on 1) Markov Decision Process (MDP), 2) Multimodal Route Planning, and 3) Hierarchical Stochastic Planning, Choudhury created an algorithm called **DreamrHHP**(Dynamic Real-time Multimodal Routing with Hierarchical Hybrid Planning)

* MDP

  ![MDP figure.png](/assets/images/posts/2022-06-11/3-A-3_MDP_figure.png){: width="250" height="250"}{: .align-center}
  ![MDP.png](/assets/images/posts/2022-06-11/3-A-2_mdpmdp.png){: .align-center}


## B) This Study

**1)  Route Planning**
  * Apply data analysis-based distribution to the calculation of ETA(estimated time of arrival)
  * Choudhury et al. (2019) updates the changing state and applies A* heuristic search to repeatedly plan the route of drone
  * Review the multimodal route planning methodology for better objective function values (minimizing delivery time)

  ![Route Planning.png](/assets/images/posts/2022-06-11/3-B-1_RP.png){: .align-center}

**2) Optimization of Multiple Demand Delivery**

  ![Multiple Demands.png](/assets/images/posts/2022-06-11/3-B-2_MultipleDemands.png){: .align-center}

* Use public transportation vehicles to assist with the movement of goods to deliver multiple demand quickly
* Which vehicles should be loaded with which parcels and when to improve delivery efficiency
* By introducing a drone charging system using public transportation, multiple demand delivery can be carried out efficiently

**3) Multiple Drones**

  ![Multiple Drones.png](/assets/images/posts/2022-06-11/3-B-3_MultipleDrones.png){: .align-center}

Which drone will deliver the parcel?
When to deliver the parcel?

# 4. Data

## A) Introduction of Data

**(1) Bus Route Information Data**

**Data description**

* Source: Seoul bus route information OpenAPI
* Spatial scope of data: 8 bus routes that pass through Songpa-gu
  * bus route num : 303, 340, 341, 401, 3313, 3412, 3414, 3417

**Example of raw data**
![Raw Data.png](/assets/images/posts/2022-06-11/4-A-2_RouteInfo.png)

Description of key variables
* seq : The order of sections of a bus route (= sectOrd column of bus location data)
* section : The id of a section (= sectionId column of bus location data)

**Visualization - bus route**

![Bus Route.png](/assets/images/posts/2022-06-11/4-C-1_BusRoute.png){: width="350" height="350"}



**(2) Bus Location Data**

**Data description**

* Source: Seoul bus location information OpenAPI
* Spatial scope of data: 8 bus routes that pass through Songpa-gu
  * bus route num : 303, 340, 341, 401, 3313, 3412, 3414, 3417
* Temporal scope of data: 06:00 ~ 24:00, every day
* Daily data are classified by bus route, bus vehicle ID, vehicle trip, and direction through preprocessing

**Example of raw data**
![Raw Data.png](/assets/images/posts/2022-06-11/4-A-1_BusLoc.png)

**Description of key variables**
* runTm : The time when the api was called for data collection
* dataTm : The time when the location information(coordinates) of the bus was recorded
* sectOrd : The order of sections of a bus route (= seq column of bus route information data)
* sectionId : The id of a section (= section column of bus route information data)

**Visualization - bus route & bus location**

![Bus Route Location.png](/assets/images/posts/2022-06-11/4-C-2_BusRouteLoc.png){: width="900" height="450"}

![Bus Velocity.png](/assets/images/posts/2022-06-11/4_3d2.png){: width="600" height="300"}{: .align-center}

## B) EDA

[4. Data - EDA](https://sh38ryu.github.io/coding/data_EDA/)



# 5. Experimental Results

**Single Demand (Choudhury et al.)**

![Experimental Results.png](/assets/images/posts/2022-06-11/5-1_ExpRes_single.png){: width="250" height="400"}{: .align-center}

![Experimental Results.png](/assets/images/posts/2022-06-11/5-1_ExpRes.png)



# 6. Conclusion

* There are many constraints on drone delivery, but efforts are being made to activate it with the great advantages of **reducing delivery time**, reducing costs, and being environmentally friendly
* Since drone movement is different from existing transportation methods, a lot of research on the system is required to introduce drone delivery
* Greater synergy is expected when drones are used in combination with public transportation
* Research Plan : Route Planning, Optimization of Multiple Demand Delivery, Multiple Drones


# References
* Literature Review
  * Huang, H., Savkin, A. V., & Huang, C. (2020). Scheduling of a parcel delivery system consisting of an aerial drone interacting with public transportation vehicles. Sensors, 20(7), 2045.
  * Huang, H., Savkin, A. V., & Huang, C. (2020). Reliable path planning for drone delivery using a stochastic time-dependent public transportation network. IEEE Transactions on Intelligent Transportation Systems, 22(8), 4941-4950.
  * Huang, H., Savkin, A. V., & Huang, C. (2020). Drone routing in a time-dependent network: Toward low-cost and large-range parcel delivery. IEEE Transactions on Industrial Informatics, 17(2), 1526-1534.
  * Huang, H., Savkin, A. V., & Huang, C. (2020). Drone routing in a time-dependent network: Toward low-cost and large-range parcel delivery. IEEE Transactions on Industrial Informatics, 17(2), 1526-1534.
  * Choudhury, S., Knickerbocker, J. P., & Kochenderfer, M. J. (2019, June). Dynamic real-time multimodal routing with hierarchical hybrid planning. In 2019 IEEE Intelligent Vehicles Symposium (IV) (pp. 2397-2404). IEEE.
  * Choudhury, S., Solovey, K., Kochenderfer, M. J., & Pavone, M. (2021). Efficient large-scale multi-drone delivery using transit networks. Journal of Artificial Intelligence Research, 70, 757-788.
  * Jin, Y., Xu, J., Wu, S., Xu, L., Yang, D., & Xia, K. (2021). Bus network assisted drone scheduling for sustainable charging of wireless rechargeable sensor network. Journal of Systems Architecture, 116, 102059.
  * Pan, Y., Li, S., Chen, Q., Zhang, N., Cheng, T., Li, Z., ... & Zhu, T. (2021). Efficient Schedule of Energy-Constrained UAV Using Crowdsourced Buses in Last-Mile Parcel Delivery. Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies, 5(1), 1-23.
  * Moadab, A., Farajzadeh, F., & Fatahi Valilai, O. (2022). Drone routing problem model for last-mile delivery using the public transportation capacity as moving charging stations. Scientific Reports, 12(1), 1-16.
  * Rahman, M. M., Wirasinghe, S. C., & Kattan, L. (2018). Analysis of bus travel time distributions for varying horizons and real-time applications. Transportation Research Part C: Emerging Technologies, 86, 453-466.
* Website
  * 당잃배송. (2022, June 12). Gettyimagebank. https://m.gettyimagesbank.com/view/%EA%B0%80%EC%A0%95%EC%9D%98%EB%8B%AC-5%EC%9B%94-%EA%B0%80%EC%A1%B1-%EC%9D%BC%EB%9F%AC%EC%8A%A4%ED%8A%B8/a10998285
  * 11번가도 ’쓱~’… 수도권 지역 SSG닷컴 “새벽배송” 서비스 도입. (2022, June 12). 뉴데일리경제. https://biz.newdaily.co.kr/site/data/html/2021/01/11/2021011100101.html
  * “새벽보다 빠른 야간배송, 365일 최저가까지”…유통家 생존전쟁 ‘점입가경.’ (2022, June 12). 동아일보. https://www.donga.com/news/Economy/article/all/20190806/96846449/1
  * ★가네샤요가프랍스 쿠팡 로켓배송 입점★ ▶가네샤 요가매트 구매하고 인증하면 ’가네샤 요가 핸드타월’을 드려요! (2022, June 12). 가네샤요가프랑스. https://www.ganeshayogaprops.com/52/?q=YToyOntzOjQ6InBhZ2UiO2k6NDtzOjEyOiJrZXl3b3JkX3R5cGUiO3M6MzoiYWxsIjt9&bmode=view&idx=5351957&t=board
  * We’re Bringing the Convenience of Drone Delivery to 4 Million U.S. Households in Partnership with DroneUp. (2022, June 12). Walmart. https://corporate.walmart.com/newsroom/2022/05/24/were-bringing-the-convenience-of-drone-delivery-to-4-million-u-s-households-in-partnership-with-droneup
  * UPS Has a Delivery Truck That Can Launch a Drone. (2022, June 12). THE VERGE. URL: https://www.theverge.com/2017/2/21/14691062/ups-drone-delivery-truck-test-completed-video
  * 도미노피자, 국내 최초 드론 배달 서비스 상용화. (2022, June 12). 식품외식경제. https://www.foodbank.co.kr/news/articleView.html?idxno=61821
  * 유통 ‘배송전쟁’ 롯데·신세계도 뛰어들어…이커머스 업계 “해볼만”. (2022.01.04). URL: https://www.enewstoday.co.kr/news/articleView.html?idxno=1327399
  * 코로나19 위기 속 안전하면서도 편리한 배송 ‘드론’. (2022.01.04). URL: https://www.klnews.co.kr/news/articleView.html?idxno=121867
  * [드론배송, 어디까지 왔나-②] 기업이 끌고 국가가 민다···세계는 상용화 잰걸음. (2022.01.04). URL: http://www.todaykorea.co.kr/news/articleView.html?idxno=294303
  * [드론배송, 어디까지 왔나-③] 한국에는 먼 미래?···한계 지적도. (2022.01.04). URL: http://www.todaykorea.co.kr/news/articleView.html?idxno=294304
  * 세계는 지금 라스트마일 전쟁 중[이코노미 조선]. (2021.05.05). URL: http://economy.chosun.com/client/news/view.php?boardName=C00&t_num=13606055
  * 카카오맵. (2022, May 24). URL: https://map.kakao.com/
