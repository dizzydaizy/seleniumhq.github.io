---
title: "ブラウザーのドライバーをインストールする"
linkTitle: "ブラウザーのドライバーをインストールする"
weight: 4
needsTranslation: true
description: >
  自動化するブラウザを設定する。
aliases: [
"/documentation/ja/selenium_installation/installing_webdriver_binaries/",
"/documentation/ja/webdriver/driver_requirements/",
"/ja/documentation/getting_started/installing_browser_drivers/"
]
---

Seleniumは、WebDriverを介して、Chrome/Chromium、Firefox、Internet Explorer、Edge、Opera、Safari
などの市場にあるすべての主要なブラウザーをサポートします。 
可能な場合、WebDriverは、ブラウザーに組み込まれている自動化のサポートを使用してブラウザーを動かします。

Internet Explorerを除くすべてのドライバーの実装は、ブラウザーベンダー自身によって提供されているため、
標準のSeleniumディストリビューションには含まれていません。 
この章では、さまざまなブラウザを使い始めるための基本的な要件について説明します。

Read about more advanced options for starting a driver
in our [driver configuration]({{< ref "/documentation/webdriver/drivers.md" >}}) documentation.

## クイックリファレンス

| ブラウザー | サポートするOS | 維持管理機関 | ダウンロード | イシュートラッカー |
| ------- | ------------ | ------------- | -------- | ------------- |
| Chromium/Chrome | Windows/macOS/Linux | Google | [Downloads](//chromedriver.storage.googleapis.com/index.html) | [Issues](//bugs.chromium.org/p/chromedriver/issues/list) |
| Firefox | Windows/macOS/Linux | Mozilla | [Downloads](//github.com/mozilla/geckodriver/releases) | [Issues](//github.com/mozilla/geckodriver/issues) |
| Edge | Windows/macOS | Microsoft | [Downloads](//developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/) | [Issues](https://github.com/MicrosoftDocs/edge-developer/issues) |
| Internet Explorer | Windows | Selenium Project | [Downloads](/downloads) | [Issues](//github.com/SeleniumHQ/selenium/labels/D-IE) |
| Safari | macOS High Sierra and newer | Apple | Built in | [Issues](//bugreport.apple.com/logon) |

Note: The Opera driver does not support w3c syntax, so we recommend using chromedriver to work with Opera.
See the code example for [opening an Opera browser]({{< ref "open_browser.md#opera" >}})

## ドライバーを使用する3つの方法

### 1. ドライバー管理ソフトウェア

ほとんどのマシンはブラウザを自動的に更新しますが、ドライバは更新しません。
ブラウザに適切なドライバを確実に入手するために、多くのサードパーティライブラリが役立ちます。

{{< tabpane langEqualsHeader=true >}}
{{< tab header="Java" >}}

// Use WebDriver Manager: https://github.com/bonigarcia/webdrivermanager

// Import WebDriver Manager:
import io.github.bonigarcia.wdm.WebDriverManager;

// Call setup() method for the browser driver you want:
WebDriverManager.chromedriver().setup();

// Initialize your driver as you normally would:
ChromeDriver driver = new ChromeDriver();

{{< /tab >}}
{{< tab header="Python" >}}

# Use Webdriver Manager for Python: https://github.com/SergeyPirogov/webdriver_manager

# Import code:
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service

# Use the `install()` method to set `executabe_path` in a new `Service` instance:
service = Service(executable_path=ChromeDriverManager().install())

# Pass in the `Service` instance with the `service` keyword: 
driver = webdriver.Chrome(service=service)

{{< /tab >}}
{{< tab header="CSharp" >}}
// Use WebDriver Manager Package: https://github.com/rosolko/WebDriverManager.Net

// Import the dependencies:
using WebDriverManager;
using WebDriverManager.DriverConfigs.Impl;

// Use the `SetUpDriver()` which requires a config class:
new DriverManager().SetUpDriver(new ChromeConfig());

// Initialize your driver as you normally would:
var driver = new ChromeDriver()

{{< /tab >}}
{{< tab header="Ruby" >}}
# Use webdrivers gem: https://github.com/titusfortner/webdrivers

# Add gem to Gemfile:
gem 'webdrivers', '~> 5.0'

# Require webdrivers in your project:
require 'webdrivers'

# Initialize driver as you normally would:
driver = Selenium::WebDriver.for :chrome

{{< /tab >}}
{{< tab header="JavaScript" >}}
// There is not a recommended driver manager for JavaScript at this time
{{< /tab >}}
{{< tab header="Kotlin" >}}
// Use WebDriverManager: https://github.com/bonigarcia/webdrivermanager

// Import the library
import io.github.bonigarcia.wdm.WebDriverManager

// Call the setup method before initializing the driver as you normally would:
fun chrome(): WebDriver {
    WebDriverManager.chromedriver().setup()
    return ChromeDriver()
}
{{< /tab >}}
{{< /tabpane >}}

### 2. `PATH` 環境変数
このオプションでは、最初に手動でドライバーをダウンロードする必要があります
（リンクについては[クイックリファレンス](#クイックリファレンス)を参照してください）。

これは、コードを更新せずにドライバーの場所を変更するための柔軟なオプションであり、各マシンがドライバーを同じ場所に配置する必要なく、複数のマシンで機能します。

`PATH` にすでにリストされているディレクトリにドライバを配置するか、ディレクトリに配置して `PATH` に追加することができます。

* すでに `PATH` にあるディレクトリを確認するには、コマンドプロンプト/ターミナルを開いて次のように入力します。

{{< tabpane  >}}
{{< tab header="Mac / Linux" >}}
echo $PATH 
{{< /tab >}}
{{< tab header="Windows" >}}
echo %PATH%
{{< /tab >}}
{{< /tabpane >}}

<br />
* ドライバを配置するディレクトリがまだPATHにない場合は、次のディレクトリを追加する必要があります。

{{< tabpane  >}}
{{< tab header="Mac / Linux" >}}
export PATH=$PATH:/opt/WebDriver/bin >> ~/.profile
{{< /tab >}}
{{< tab header="Windows" >}}
setx PATH "%PATH%;C:\WebDriver\bin"
{{< /tab >}}
{{< /tabpane >}}

<br />
* ドライバを起動することで、正しく追加されているかどうかをテストできます。

 ```shell
  chromedriver
  ```

* If your `PATH` is configured correctly,
* `PATH` が正しく構成されている場合、ドライバーの起動に関連する出力が表示されます。

```
Starting ChromeDriver 95.0.4638.54 (d31a821ec901f68d0d34ccdbaea45b4c86ce543e-refs/branch-heads/4638@{#871}) on port 9515
Only local connections are allowed.
Please see https://chromedriver.chromium.org/security-considerations for suggestions on keeping ChromeDriver safe.
ChromeDriver was started successfully.
```

 <kbd>Ctrl+C</kbd> を押して、コマンドプロンプトの制御を取り戻すことができます。

### 3. ハードコードされた場所

上記のオプション2と同様に、ドライバーを手動でダウンロードする必要があります。
（リンクについては [クイックリファレンス](#クイックリファレンス) を参照してください）。 
コードそのものに場所を指定することには、システム上の環境変数を把握する必要がないという利点がありますが、
コードの柔軟性が大幅に低下するという欠点があります。

{{< tabpane langEqualsHeader=true >}}

{{< tab header="Java" >}}

System.setProperty("webdriver.chrome.driver","/opt/WebDriver/bin/chromedriver");
ChromeDriver driver = new ChromeDriver();

{{< /tab >}}

{{< tab header="Python" >}}

service = Service(executable_path="/opt/WebDriver/bin/chromedriver")
driver = webdriver.Chrome(service=service)

{{< /tab >}}

{{< tab header="CSharp" >}}

var driver = new ChromeDriver(@"C:\WebDriver\bin");

{{< /tab >}}

{{< tab header="Ruby" >}}

service = Selenium::WebDriver::Service.chrome(path: '/opt/WebDriver/bin/chromedriver')
driver = Selenium::WebDriver.for :chrome, service: service

{{< /tab >}}

{{< tab header="JavaScript" >}}
const {Builder} = require('selenium-webdriver');
const chrome = require('selenium-webdriver/chrome');

const service = new chrome.ServiceBuilder('/opt/WebDriver/bin/chromedriver');
const driver = new Builder().forBrowser('chrome').setChromeService(service).build();
{{< /tab >}}

{{< tab header="Kotlin" >}}

// Please raise a PR to add code sample

{{< /tab >}}

{{< /tabpane >}}


## ブラウザの起動

### Chromium/Chrome

デフォルトでは、Selenium4はChromev75以降と互換性があります。 
Chromeのバージョンとchromedriverのバージョンはメジャーバージョンと一致する必要があることに注意してください。 
該当するダウンロードリンクについては、[クイックリファレンス](#クイックリファレンス)を参照してください。

Chromeの起動方法の例は、前章、つまり詳しく説明した[ドライバーを使用する3つの方法](#ドライバーを使用する3つの方法)に記載されています。


{{< tabpane langEqualsHeader=true >}}
{{< tab header="Java" >}}
System.setProperty("webdriver.chrome.driver","/path/to/chromedriver");
ChromeDriver driver = new ChromeDriver();
{{< /tab >}}

{{< tab header="Kotlin" >}}
import org.openqa.selenium.chrome.ChromeDriver

fun main(args: Array<String>) {
  System.setProperty("webdriver.chrome.driver", "/path/to/chromedriver")
  val driver = ChromeDriver()
}
{{< /tab >}}

{{< /tabpane >}}

### Edge

Microsoft Edgeは、サポートされている最も古いバージョンのv79を使用してChromiumで実装されています。 
Chromeと同様に、Edgeのバージョンとedgedriverのバージョンはメジャーバージョンと一致する必要があります。 
該当するダウンロードリンクについては、[クイックリファレンス](#クイックリファレンス)を参照してください。

{{< tabpane langEqualsHeader=true >}}
{{< tab header="Java" >}}
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.edge.EdgeDriver;

WebDriver driver = new EdgeDriver();
{{< /tab >}}
{{< tab header="Python" >}}
from selenium.webdriver import Edge

driver = Edge()
{{< /tab >}}
{{< tab header="CSharp" >}}
using OpenQA.Selenium;
using OpenQA.Selenium.Firefox;

IWebDriver driver = new EdgeDriver();
{{< /tab >}}
{{< tab header="Ruby" >}}
require "selenium-webdriver"

driver = Selenium::WebDriver.for :edge
{{< /tab >}}
{{< tab header="JavaScript" >}}
const {Builder} = require('selenium-webdriver');

var driver = new Builder().forBrowser('edge').build();
{{< /tab >}}
{{< tab header="Kotlin" >}}
import org.openqa.selenium.WebDriver
import org.openqa.selenium.Edge.EdgeDriver

val driver: WebDriver = EdgeDriver()
{{< /tab >}}
{{< /tabpane >}}

### Firefox

Selenium4にはFirefox78以降が必要です。 
常に最新バージョンのgeckodriverを使用することをお勧めします。 
該当するダウンロードリンクについては、[クイックリファレンス](#クイックリファレンス)を参照してください。

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;

WebDriver driver = new FirefoxDriver();
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver import Firefox

driver = Firefox()
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using OpenQA.Selenium;
using OpenQA.Selenium.Firefox;

IWebDriver driver = new FirefoxDriver();
  {{< /tab >}}
  {{< tab header="Ruby" >}}
require "selenium-webdriver"

driver = Selenium::WebDriver.for :firefox
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const {Builder} = require('selenium-webdriver');

var driver = new Builder().forBrowser('firefox').build();
 {{< /tab >}}
  {{< tab header="Kotlin" >}}
import org.openqa.selenium.WebDriver
import org.openqa.selenium.Firefox.FirefoxDriver

val driver: WebDriver = FirefoxDriver()
  {{< /tab >}}
{{< /tabpane >}}


### Internet Explorer

Seleniumプロジェクトは、 [Microsoftがカレントバージョンとみなすもの](//support.microsoft.com/en-gb/help/17454/lifecycle-support-policy-faq-internet-explorer) 
と同じリリースをサポートすることを目的としています。 
古いリリースは機能する可能性がありますが、サポートされません。 
Internet Explorer 11は、2022年6月15日にWindows 10を含む特定のオペレーティングシステムのサポートを終了することに注意してください。Edgeには、引き続きサポートされるIE互換モードがあります。

IEドライバーは、Seleniumプロジェクトによって直接維持される唯一のドライバーです。 
Internet Explorerの32ビットバージョンと64ビットバージョンの両方のバイナリを使用できますが、
64ビットドライバーにはいくつかの[制限](//jimevansmusic.blogspot.co.uk/2014/09/screenshots-sendkeys-and-sixty-four.html)があります。 
そのため、32ビットドライバを使用することをお勧めします。 
Internet Explorerの設定はログインしたユーザーのアカウントに対して保存されるため、追加の設定が必要になることに注意してください。

Internet Explorerの使用に関する追加情報は、[Selenium wiki](//github.com/SeleniumHQ/selenium/wiki/InternetExplorerDriver)にあり、
該当するダウンロードリンクの[クイックリファレンス](#クイックリファレンス)を参照してください。

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.ie.InternetExplorerDriver;

WebDriver driver = new InternetExplorerDriver();
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver import Ie

driver = Ie()
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using OpenQA.Selenium;
using OpenQA.Selenium.IE;

IWebDriver driver = new InternetExplorerDriver();
  {{< /tab >}}
  {{< tab header="Ruby" >}}
require "selenium-webdriver"

driver = Selenium::WebDriver.for :ie
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const {Builder} = require('selenium-webdriver');

var driver = new Builder().forBrowser('internet explorer').build();
 {{< /tab >}}
  {{< tab header="Kotlin" >}}
import org.openqa.selenium.WebDriver
import org.openqa.selenium.ie.InternetExplorerDriver

val driver: WebDriver = InternetExplorerDriver()
  {{< /tab >}}
{{< /tabpane >}}

### Opera

Operaの現在のリリースはChromiumエンジン上に構築されており、
WebDriverはクローズドソースの [Opera Chromium Driver](//github.com/operasoftware/operachromiumdriver/releases) を介してサポートされるようになりました。

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.opera.OperaDriver;

WebDriver driver = new OperaDriver();
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver import Opera

driver = Opera()
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using OpenQA.Selenium;
using OpenQA.Selenium.Opera;

IWebDriver driver = new OperaDriver();
  {{< /tab >}}
  {{< tab header="Ruby" >}}
# Not currently implemented
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const {Builder} = require("selenium-webdriver");

var driver = new Builder().forBrowser('opera').build();
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
import org.openqa.selenium.WebDriver
import org.openqa.selenium.opera.OperaDriver

val driver: WebDriver = OperaDriver()
  {{< /tab >}}
{{< /tabpane >}}

### Safari

ChromiumおよびFirefoxドライバーとは異なり、safaridriverはオペレーティングシステムとともにインストールされます。 
Safariで自動化を有効にするには、ターミナルから次のコマンドを実行します。

```shell
safaridriver --enable
```

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.safari.SafariDriver;

WebDriver driver = new SafariDriver();
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver import Safari

driver = Safari()
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using OpenQA.Selenium;
using OpenQA.Selenium.Safari;

IWebDriver driver = new SafariDriver();
  {{< /tab >}}
  {{< tab header="Ruby" >}}
require "selenium-webdriver"

driver = Selenium::WebDriver.for :safari
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const {Builder} = require('selenium-webdriver');

var driver = new Builder().forBrowser('safari').build();
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
import org.openqa.selenium.WebDriver
import org.openqa.selenium.safari.SafariDriver

val driver: WebDriver = SafariDriver()
  {{< /tab >}}
{{< /tabpane >}}

iOSでSafariを自動化することを検討している人は、[Appiumプロジェクト](//appium.io/)を検討する必要があります。
