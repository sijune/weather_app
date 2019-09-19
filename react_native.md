# 리액트 문법으로 모바일 개발하기

### 리액트 네이티브
***모든 것을 오브젝트로 작성한다.***<br>
+ 리액트 네이티브는 리턴할 컴포넌트가 한정되어 있다.
+ ex. JS코드 => java나 Object-C로 바뀐다.
+ 이는 리액트 네이티브 공식사이트에서 확인 가능<br>

+ 장점
	+ 리턴하는 값이 웹과 다르다.
	+ 앱 디자인을 flexbox로 가능
	+ 네이티브 코드(자바나 Swift))로 작성하면 어렵다.<br>

+ 단점
	+ 리액트 네이티브는 문법에 엄격하다.
	+ 모든 것을 문법 태그내에 작성해야 한다.

--------------------------------------------------------------------------------

### Expo와 그 특징

+ 우리가 js로 코딩한 react컴포넌트는 react native플랫폼을 거쳐 ios, android native코드로<br> 
각각 변환된다.
+ 이를 쉽게 해주는 게 expo다.<br>

+ react native기반 expo라는 툴을 쓸거다.
+ 앱을 쉽게 개발할 수 있게 만들어 줄꺼다.
+ expo는 쉽게 테스트도 빠르게 가능, 귀찮은 과정을 다 스킵한다.
  + 코드자체를 앱스토어에 올리는 게 아니라<br>
앱이 열릴때마다 서버에 있는 코드를 받아서 실행한다.<br>

+ 코드를 잘못작성하면 에러발생. react에 비해 엄격하다.0
+ 무조건 정해진대로 작성해야하다.<br>

+ 자기가 알아서 npm, reactnative를 다운 받는다.
+ 모바일 환경에서 확인 - device - android
+ 로그확인도 가능
+ expo client 로 qr코드 스캔, 첫번째로 열땐 시간이 조금 걸린다.
+ 핫리로딩 : 변경된 부분만 새로고침한다. 전체를 새로고침하지 않는다.<br>

+ 안드로이드로 빌드할 예정
+ 안드로이드 시뮬레이터로 테스트 할꺼다.<br>

+ IOS와 Android 사이에 코드 공유가 가능

-----------------------------------------------------------

### React
+ UI를 만들기 위한 JS라이브러리, MVC에서 View에 집중

### ReactNative
+ React로 네이티브 모바일 앱을 만들 수 있게 도와주는 라이브러리
+ 리액트 네이티브로 작성된 코드를 컴파일한 결과는 결국 objectC나 java다.
+ 우리는 jsx로 작성 페이스북 기술에 의해 js-objectiveC, js-java가 구동

#### 사용된 예시 : 인스타그램, 페이스북, 에어비앤비 등 어플에서 사용<br>

### 자주 나오는 개념
***function, state, component*** 

### 한정된 컴포넌트만 사용가능
+ reactnative는 리턴할 수 있는 컴포넌트가 한정되어 있다.
+ import로 삽입된 한정된 컴포넌트만 리액트 네이티브가 native로 바꿔준다.
+ html,css둘다 정해진 패턴이 있다.

--------------------------------------------------------------------

### 환경설정

```bash
node -v //nodejs가 버전10이상이여야 한다.
```
npm은 자동 설치<br>
yarn도 설치하자<br>
+ yarn이란?
	+ npm의 느린 속도로 페이스북, 구글 개발자들이 만들 패키지 매니저
	+ expo init kawai_todo 를 할 때, yarn을 이용해 설치된다.<br>
```bash
$ npm install --global yarn //오류 시 환경변수 확인, warn이 떠도 상관x
```


```bash
$ npm install expo-cli --global
$ expo init hello_weather //첫번째 템플릿 선택, 이름은 hello_weather
$ cd hello_weather
$ expo start
```

## 모바일 화면을 실행하는 방법 
1. expo 앱을 깔고 qr코드 스캔, 단 같은 네트워크에 있어야 됨 - 핫스팟을 통해 가능
2. 안드로이드 스튜디오 깔기
https://docs.expo.io/versions/v34.0.0/workflow/android-studio-emulator/ 참고<br>
환경변수로 ANDROID_HOME, sdk경로 추가해주기<br>
에뮬레이터를 실행시키고, expo start, Run on Android device 클릭<br>

##### 핫리로딩 설정가능
1. 모바일이라면 - shake <br>
2. 에뮬레이터라면 - ctrl + m<br> 



## 깃 저장소 생
``` bash
$ git init
$ git remote ~~
$ git pull origin master //먼저 땡겨온다.
//안되면 git pull origin (branchname) --allow-unrelated-histories 쓰기(강제로 땡겨온다)
$ git add .
$ git commit -m "first commit"
$ git push origin master
```

### 환경설정 끝

-----------------------------------------------------------------

local state로 작업해야 한다.

***state가 변경되면 render를 다시한다.***
 
로딩 화면 만들기

-App.js
import React, {Component} from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default class App extends Component{
  state = {
    //정보를 받았느지 안받았는지 알려주는 indicator가 필요
    //데이터 api를 불러오면 이 값은 true가 될 것이다.
    isLoaded: false
  }
  render() {
    const { isLoaded } = this.state;
    return (
      <View style={styles.container}>
        {/* 로딩이 완료되면 정보, 로딩이 완료되지않으면 로딩뷰 */}
        {isLoaded ? null : 
          <View style = {styles.loading}>
            <Text style={styles.loadingText}>Hello, this is Hello Weather App!</Text>
          </View>}
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  },
  loading: {
    flex: 1,
    backgroundColor: "#FDF6AA",
    justifyContent: 'flex-end',
    paddingLeft: 25
  },
  loadingText:{
    fontSize: 30,
    marginBottom: 100,

  }
});

------------------------------------------
날씨화면을 만들꺼다.

expo install expo-linear-gradient

-App.js
import React, {Component} from 'react';
import { StyleSheet, Text, View } from 'react-native';

import Weather from "./weather";

export default class App extends Component{
  state = {
    //정보를 받았느지 안받았는지 알려주는 indicator가 필요
    //데이터 api를 불러오면 이 값은 true가 될 것이다.
    isLoaded: true
  }
  render() {
    const { isLoaded } = this.state;
    return (
      <View style={styles.container}>
        {/* 로딩이 완료되면 정보, 로딩이 완료되지않으면 로딩뷰 */}
        {isLoaded ? <Weather /> : 
          <View style = {styles.loading}>
            <Text style={styles.loadingText}>Hello, this is Hello Weather App!</Text>
          </View>}
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  },
  loading: {
    flex: 1,
    backgroundColor: "#FDF6AA",
    justifyContent: 'flex-end',
    paddingLeft: 25
  },
  loadingText:{
    fontSize: 30,
    marginBottom: 100,

  }
});

-weather.js
import React, {Component} from 'react';
import {StyleSheet, Text, View } from 'react-native';
import {LinearGradient} from "expo-linear-gradient";
//백그라운드가 그라디언트다.

export default class Weather extends Component {
    render() {
        return (
            //Linear gradient의 2가지 property이 필요: 색상, 스타일
            <LinearGradient
             colors={["#00C6FB", "#0058EA"]} //from-to
             style={styles.container} 
             >
                <View style={styles.upper} >
                     <Text>Icon</Text>
                     <Text style={styles.temp}>35</Text>
                 </View>
                 <View style={styles.lower}>
                    <Text style={styles.title}>무섭게 비오는 중</Text>
                    <Text style={styles.subtitle}>For more info look outside</Text>
                 </View>
             </LinearGradient>
        )
       
    }
}

const styles = StyleSheet.create({
    container: {
        flex:1
    },
    upper: {
        flex:1,
        alignItems:"center",
        justifyContent:"center"
    },
    temp: {
        fontSize:38,
        backgroundColor: "transparent",
        color: "white",
        marginTop:10
    },
    lower: {
        flex:1,
        alignItems: "flex-start",
        justifyContent: "flex-end",
        paddingLeft:25,

    },
    title: {
        fontSize:38,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 10,
        fontWeight: "300"
    },
    subtitle: {
        fontSize:24,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 24
    }
})

---------------------------------------
아이콘 만들기

{/* 상단을 다 없애준다. 리액트에서 제공하는 api */}
        <StatusBar hidden={true} />        

expo에서는 아이콘을 api로 제공해준다.
https://expo.github.io/vector-icons/

이중에서 MaterialCommunityIcons를 쓴다.
(원래 강의는 Ionicons를 쓰지만 끝에 MaterialCommunityIcons로 수정됨)




-App.js
import React, {Component} from 'react';
import { StyleSheet, Text, View, StatusBar } from 'react-native';

import Weather from "./weather";

export default class App extends Component{
  state = {
    //정보를 받았느지 안받았는지 알려주는 indicator가 필요
    //데이터 api를 불러오면 이 값은 true가 될 것이다.
    isLoaded: true
  }
  render() {
    const { isLoaded } = this.state;
    return (
      <View style={styles.container}>
        {/* 상단을 다 없애준다. 리액트에서 제공하는 api */}
        <StatusBar hidden={true} />        
        {/* 로딩이 완료되면 정보, 로딩이 완료되지않으면 로딩뷰 */}
        {isLoaded ? <Weather /> : 
          <View style = {styles.loading}>
            <Text style={styles.loadingText}>Hello, this is Hello Weather App!</Text>
          </View>}
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  },
  loading: {
    flex: 1,
    backgroundColor: "#FDF6AA",
    justifyContent: 'flex-end',
    paddingLeft: 25
  },
  loadingText:{
    fontSize: 30,
    marginBottom: 100,

  }
});

-weather.js
import React, {Component} from 'react';
import {StyleSheet, Text, View } from 'react-native';
import {LinearGradient} from "expo-linear-gradient";
//백그라운드가 그라디언트다.
import { Ionicons} from "@expo/vector-icons";
//폰트 어썸도 불러올 수 있다.

export default class Weather extends Component {
    render() {
        return (
            //Linear gradient의 2가지 property이 필요: 색상, 스타일
            <LinearGradient
             colors={["#00C6FB", "#0058EA"]} //from-to
             style={styles.container} 
             >
                <View style={styles.upper} >
                    {/* 속성변경 가능 */}
                   <Ionicons color="white" size={144} name="ios-rainy" />
                     <Text style={styles.temp}>35</Text>
                 </View>
                 <View style={styles.lower}>
                    <Text style={styles.title}>무섭게 비오는 중</Text>
                    <Text style={styles.subtitle}>For more info look outside</Text>
                 </View>
             </LinearGradient>
        )
       
    }
}

const styles = StyleSheet.create({
    container: {
        flex:1
    },
    upper: {
        flex:1,
        alignItems:"center",
        justifyContent:"center",
        backgroundColor: "transparent" //부모 컴포넌트가 transparent가 되어야 자식컴포넌트가 보인다.
    },
    temp: {
        fontSize:48,
        backgroundColor: "transparent",
        color: "white",
        marginTop:10
    },
    lower: {
        flex:1,
        alignItems: "flex-start",
        justifyContent: "flex-end",
        paddingLeft:25,

    },
    title: {
        fontSize:38,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 10,
        fontWeight: "300"
    },
    subtitle: {
        fontSize:24,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 24
    }
})

--------------------------------------------------------
자바스크립트는 유저의 위치를 navigator를 이용해 현재 위치를 뽑아준다.
navigator.geolocation.getCurrentPosition(function(position){
	console.log(position)
})
=>위치정보
getCurrentPosition가 성공적으로 수행하면 한개의 함수를 실행한다.
그 안에 하나의 attribute가 있는데 그게 위치정보를 갖는다.

리액트 네이티브에서도 동일하게 작동

***위치정보와 날씨가 확인되면 isLoaded를 true로 변경한다.***

   
-App.js
  componentDidMount() {
    navigator.geolocation.getCurrentPosition(
      position => {
        console.log(position)
      }
    )
  }
우선 확인

-App.js
  state = {
    //정보를 받았느지 안받았는지 알려주는 indicator가 필요
    //데이터 api를 불러오면 이 값은 true가 될 것이다.
    isLoaded: false,
    
  }
  componentDidMount() {
    navigator.geolocation.getCurrentPosition(
      position => {
        this.setState({
          isLoaded:true
        })
      },
      error=>{
        console.log(error)
      }
    )
  }

-------------------------------------------------
이 위치를 api로 보낸다 그 api로 날싸정보를 얻어서 보여줄 수 있다.

날씨 api가 필요 open weather map
회원가입 필요
api키: f7538a75367b9b9f43e4fdc306c4a5ab

CONST API_KEY = "~~";
키와 lat, lon으로 날씨정보를 받아온다.

***위치정보와 날씨가 확인되면 isLoaded를 true로 변경한다.***

앱에서 debug JS remotely를 클릭하면 원격으로 디버그 가능

-App.js
state = {
    //정보를 받았느지 안받았는지 알려주는 indicator가 필요
    //데이터 api를 불러오면 이 값은 true가 될 것이다.
    isLoaded: false,
    error: null,
    temperature: null,
    name: null
    
  }
  componentDidMount() {
    navigator.geolocation.getCurrentPosition(
      position => {
        //console.log(position)
        this._getWeather(position.coords.latitude, position.coords.longitude)
        },
      error=>{
        // console.log(error)
        this.setState({
          error: error
        })
      }
    )
  }
  _getWeather = (lat, lon) => {
    fetch(`http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&APPID=${API_KEY}`) //작은 따옴표가 아니라 물결 밑에 `마크다.
    .then(response=>response.json())
    .then(json => {
      this.setState({
        temperature: json.main.temp,
        name: json.weather[0].main,
        isLoaded: true
      })
    })
  }

-----------------------------------------------------------------
날씨 컴포넌트로 돌아가서 refactoring(코드 구조변경)을 해야한다.

state가 필요없고, props만 필요하기에 weather.js를 함수형으로 만든다.
아이콘, 온도, 타이틀의 변경이 이루어진다. -> props가 필요하다.
weathername과 temp를 자식 컴포넌트로 넘긴다. 그리고 이와 weatherCases를 잘 이용해서 렌더한다.

-App.js
import React, {Component} from 'react';
import { StyleSheet, Text, View, StatusBar } from 'react-native';

import Weather from "./weather";

const API_KEY = 'f7538a75367b9b9f43e4fdc306c4a5ab';

export default class App extends Component{
  state = {
    //정보를 받았느지 안받았는지 알려주는 indicator가 필요
    //데이터 api를 불러오면 이 값은 true가 될 것이다.
    isLoaded: false,
    error: null,
    temperature: null,
    name: null
    
  }
  componentDidMount() {
    navigator.geolocation.getCurrentPosition(
      position => {
        //console.log(position)
        this._getWeather(position.coords.latitude, position.coords.longitude)
        },
      error=>{
        // console.log(error)
        this.setState({
          error: error
        })
      }
    )
  }
  _getWeather = (lat, lon) => {
    fetch(`http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&APPID=${API_KEY}`) //작은 따옴표가 아니라 물결 밑에 `마크다.
    .then(response=>response.json())
    .then(json => {
      //console.log(json)
      this.setState({
        temperature: json.main.temp,
        name: json.weather[0].main,
        isLoaded: true
      })
    })
  }
  render() {
    const { isLoaded, error, temperature, name } = this.state;
    return (
      <View style={styles.container}>
        {/* 상단을 다 없애준다. 리액트에서 제공하는 api */}
        <StatusBar hidden={true} />        
        {/* 로딩이 완료되면 정보, 로딩이 완료되지않으면 로딩뷰 */}
        {isLoaded ? <Weather weatherName={name} temp = {Math.ceil(temperature - 273.15)}/> : //공식이다.
          <View style = {styles.loading}>
            <Text style={styles.loadingText}>Hello, this is Hello Weather App!</Text>
            {/* 위치가져오는 데 에러발생시 */}
            {error ? <Text style={styles.errorText}>{error}</Text>:null}
          </View>}
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  },
  errorText: {
    color:"red",
    backgroundColor: "transparent",
    marginBottom: 40
  },
  loading: {
    flex: 1,
    backgroundColor: "#FDF6AA",
    justifyContent: 'flex-end',
    paddingLeft: 25
  },
  loadingText:{
    fontSize: 30,
    marginBottom: 24,

  }
});



-Weather.js
import React, {Component} from 'react';
import {StyleSheet, Text, View } from 'react-native';
import {LinearGradient} from "expo-linear-gradient";
//백그라운드가 그라디언트다.
import { Ionicons} from "@expo/vector-icons";
//폰트 어썸도 불러올 수 있다.
import Proptypes from "prop-types";

const weatherCases = {
  Rain: {
    colors: ["#00C6FB", "#0058EA"],
    title: "Raining like a MF",
    subtitle: "For more info look outside",
    icon: "ios-rainy"
  },
  Clear: {
    colors: ["#FEF253", "#FF7300"],
    title: "Sunny as fuck",
    subtitle: "go get your ass burnt",
    icon: "ios-sunny"
  },
  Thunderstorm: {
    colors: ["#00ECBC", "#007ADF"],
    title: "Thunderstorm in the house",
    subtitle: "Actually, outside of the house",
    icon: "ios-thunderstorm"
  },
  Clouds: {
    colors: ["#D7D2CC", "#304352"],
    title: "Clouds",
    subtitle: "I know, fucking boring",
    icon: "ios-cloudy"
  },
  Snow: {
    colors: ["#7DE2FC", "#89B6E5"],
    title: "Cold as balls",
    subtitle: "Do you want to build a snowman? Fuck no.",
    icon: "ios-snow"
  },
  Drizzle: {
    colors: ["#89F7FE", "#66A6FF"],
    title: "Drizzle",
    subtitle: "Is like rain, but gay.",
    icon: "ios-rainy-outline"
  }
};


function Weather({ weatherName, temp }) {
    // console.log(typeof(weatherName)) 스트링으로 받는다.
    return (
        <LinearGradient
        colors={weatherCases[weatherName].colors} //from-to
        style={styles.container}
        >
        <View style={styles.upper}>
            {/* 속성변경 가능 */}
            <Ionicons color="white" size={144} name={weatherCases[weatherName].icon} />
            <Text style={styles.temp}>{temp}</Text>
        </View>
        <View style={styles.lower}>
            <Text style={styles.title}>{weatherCases[weatherName].title}</Text>
            <Text style={styles.subtitle}>{weatherCases[weatherName].subtitle}</Text>
        </View>
        </LinearGradient>
    );
}

Weather.propTypes = {
    temp: Proptypes.number.isRequired,
    weatherName: Proptypes.string.isRequired
}

export default Weather;

const styles = StyleSheet.create({
    container: {
        flex:1
    },
    upper: {
        flex:1,
        alignItems:"center",
        justifyContent:"center",
        backgroundColor: "transparent"
    },
    temp: {
        fontSize:48,
        backgroundColor: "transparent",
        color: "white",
        marginTop:10
    },
    lower: {
        flex:1,
        alignItems: "flex-start",
        justifyContent: "flex-end",
        paddingLeft:25,

    },
    title: {
        fontSize:38,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 10,
        fontWeight: "300"
    },
    subtitle: {
        fontSize:24,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 24
    }
})

-------------------------------------------------------
끝

-App.js
import React, {Component} from 'react';
import { StyleSheet, Text, View, StatusBar } from 'react-native';

import Weather from "./weather";

const API_KEY = 'f7538a75367b9b9f43e4fdc306c4a5ab';

export default class App extends Component{
  state = {
    //정보를 받았느지 안받았는지 알려주는 indicator가 필요
    //데이터 api를 불러오면 이 값은 true가 될 것이다.
    isLoaded: false,
    error: null,
    temperature: null,
    name: null,
    region: null
    
  }
  componentDidMount() {
    navigator.geolocation.getCurrentPosition(
      position => {
        //console.log(position)
        this._getWeather(position.coords.latitude, position.coords.longitude)
        },
      error=>{
        // console.log(error)
        this.setState({
          error: error
        })
      }
    )
  }
  _getWeather = (lat, lon) => {
    fetch(`http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&APPID=${API_KEY}`) //작은 따옴표가 아니라 물결 밑에 `마크다.
    .then(response=>response.json())
    .then(json => {
      //console.log(json)
      this.setState({
        temperature: json.main.temp,
        name: json.weather[0].main,
        region: json.name,
        isLoaded: true
      })
    })
  }
  render() {
    const { isLoaded, error, temperature, name, region } = this.state;
    return (
      <View style={styles.container}>
        {/* 상단을 다 없애준다. 리액트에서 제공하는 api */}
        <StatusBar hidden={true} />        
        {/* 로딩이 완료되면 정보, 로딩이 완료되지않으면 로딩뷰 */}
        {isLoaded ? <Weather weatherName={name} temp = {Math.ceil(temperature - 273.15)} whereyouare={region}/> : //공식이다.
          <View style = {styles.loading}>
            <Text style={styles.loadingText}>Hello, this is Hello Weather App!</Text>
            {/* 위치가져오는 데 에러발생시 */}
            {error ? <Text style={styles.errorText}>{error}</Text>:null}
          </View>}
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  },
  errorText: {
    color:"red",
    backgroundColor: "transparent",
    marginBottom: 40
  },
  loading: {
    flex: 1,
    backgroundColor: "#FDF6AA",
    justifyContent: 'flex-end',
    paddingLeft: 25
  },
  loadingText:{
    fontSize: 30,
    marginBottom: 24,

  }
});


-weather.js
import React, {Component} from 'react';
import {StyleSheet, Text, View } from 'react-native';
import {LinearGradient} from "expo-linear-gradient";
//백그라운드가 그라디언트다.
import { MaterialCommunityIcons } from "@expo/vector-icons";
//폰트 어썸도 불러올 수 있다.
import Proptypes from "prop-types";

const weatherCases = {
  Rain: {
    colors: ["#00C6FB", "#0058EA"],
    title: "Raining like a MF",
    subtitle: "For more info look outside",
    icon: "weather-rainy"
  },
  Clear: {
    colors: ["#FEF253", "#FF7300"],
    title: "Sunny as fuck",
    subtitle: "go get your ass burnt",
    icon: "weather-sunny"
  },
  Thunderstorm: {
    colors: ["#00ECBC", "#007ADF"],
    title: "Thunderstorm in the house",
    subtitle: "Actually, outside of the house",
    icon: "weather-lightning"
  },
  Clouds: {
    colors: ["#D7D2CC", "#304352"],
    title: "Clouds",
    subtitle: "I know, fucking boring",
    icon: "weather-cloudy"
  },
  Snow: {
    colors: ["#7DE2FC", "#89B6E5"],
    title: "Cold as balls",
    subtitle: "Do you want to build a snowman? Fuck no.",
    icon: "weather-snowy"
  },
  Drizzle: {
    colors: ["#89F7FE", "#66A6FF"],
    title: "Drizzle",
    subtitle: "Is like rain, but gay.",
    icon: "weather-hail"
  },
  Haze: {
    colors: ["#89F7FE", "#66A6FF"],
    title: "Haze",
    subtitle: "Don't know what that is T-T",
    icon: "weather-fog"
  },
  Mist: {
    colors: ["#D7D2CC", "#304352"],
    title: "Mist",
    subtitle: "It's like you have no glasses on.",
    icon: "weather-fog"
  }
};


function Weather({ weatherName, temp, whereyouare }) {
    // console.log(typeof(weatherName)) 스트링으로 받는다.
    return (
        <LinearGradient
        colors={weatherCases[weatherName].colors} //from-to
        style={styles.container}
        >
        <View style={styles.upper}>
            {/* 속성변경 가능 */}
            <MaterialCommunityIcons color="white" size={144} name={weatherCases[weatherName].icon} />
            <Text style={styles.temp}>{temp} ℃</Text>
        </View>
        <View style={styles.lower}>
            <Text style={styles.region}>{whereyouare}</Text>
            <Text style={styles.title}>{weatherCases[weatherName].title}</Text>
            <Text style={styles.subtitle}>{weatherCases[weatherName].subtitle}</Text>
        </View>
        </LinearGradient>
    );
}

Weather.propTypes = {
    temp: Proptypes.number.isRequired,
    weatherName: Proptypes.string.isRequired,
    whereyouare: Proptypes.string.isRequired
};

export default Weather;

const styles = StyleSheet.create({
    container: {
        flex:1
    },
    upper: {
        flex:1,
        alignItems:"center",
        justifyContent:"center",
        backgroundColor: "transparent"
    },
    temp: {
        fontSize:48,
        backgroundColor: "transparent",
        color: "white",
        marginTop:10
    },
    lower: {
        flex:1,
        alignItems: "flex-start",
        justifyContent: "flex-end",
        paddingLeft:25,

    },
    region: {
        fontSize:24,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 24
    },
    title: {
        fontSize:38,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 10,
        fontWeight: "300"
    },
    subtitle: {
        fontSize:24,
        backgroundColor: "transparent",
        color: "white",
        marginBottom: 24
    }
})





















