---
title: "Instalando bibliotecas do Selenium"
linkTitle: "Instalando bibliotecas do Selenium"
weight: 2
needsTranslation: true
description: >
  Setting up the Selenium library for your favourite programming language.
aliases: [
"/documentation/pt-br/selenium_installation/installing_selenium_libraries/",
"/pt-br/documentation/getting_started/installing_selenium_libraries/",
"/pt-br/documentation/getting_started/install_selenium_library/"
]
---

Primeiro você precisa instalar as bibliotecas Selenium para seu projeto de automação.
O processo de instalação de bibliotecas depende da linguagem que você escolher usar.

{{< tabpane disableCodeBlock=true >}}
  {{< tab header="Java" >}}
A instalação de bibliotecas Selenium para Java pode ser feita usando Maven.
Adicione a dependência selenium-java em seu pom.xml:

```xml
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-java</artifactId>
  <version>4.X</version>
</dependency>
```

A dependência _selenium-java_ suporta a execução de sua automação com todos os navegadores
com suporte Selenium. Se você quiser fazer testes
apenas em um navegador específico, você pode adicionar a dependência para esse navegador
em seu arquivo _pom.xml_.
Por exemplo, você deve adicionar a seguinte dependência em seu _pom.xml_
arquivo para executar seus testes apenas no Firefox:

```xml
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-firefox-driver</artifactId>
  <version>4.X</version>
</dependency>
```

De maneira semelhante, se você deseja executar testes apenas no Chrome,
você deve adicionar a seguinte dependência:

```xml
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-chrome-driver</artifactId>
  <version>4.X</version>
</dependency>
```
  {{< /tab >}}
  {{< tab header="Python" >}}
  A instalação de bibliotecas Selenium para Python pode ser feita usando pip:

```shell
pip install selenium
```

Como alternativa, você pode baixar o [arquivo de origem do PyPI](https://pypi.org/project/selenium/#files)
(selenium-x.x.x.tar.gz) e instale-o usando _setup.py_:

```shell
python setup.py install
```
  {{< /tab >}}
  {{< tab header="CSharp" >}}
  A instalação de bibliotecas Selenium para C# pode ser feita usando NuGet:

```shell
# Using package manager
Install-Package Selenium.WebDriver
# or using .Net CLI
dotnet add package Selenium.WebDriver
```
## Versões Suportadas .NET
Tenha certeza de utilizar a versão .NET SDK compatível com os [Pacotes Selenium](https://www.nuget.org/packages/Selenium.WebDriver) relevantes.
Veja a seção de dependências em [Versões suportadas .NET](https://dotnet.microsoft.com/en-us/download/dotnet).
Até esta atualização, .NET 5.0 (Visual Studio 2019) é suportada e .NET 6.0 não é suportada.
<br>Você pode fazer o download [MSBuild Tools 2019 aqui](https://docs.microsoft.com/en-us/visualstudio/install/create-an-offline-installation-of-visual-studio?view=vs-2019) e instalar os componentes e dependências necessárias, como .NET SDK e NuGet Package Manager.

## Usando Visual Studio Code (vscode) e C#
Este é um guia rápido para você iniciar com VSCode e C#, no entanto, mais pesquisas podem ser necessárias.
<br>Instale o .NET SDK compativel como mostrado na seção acima.
Além disso instale as extensões (Ctrl-Shift-X) C# e NuGet no VSCode.
<br>Siga as [instruções aqui](https://docs.microsoft.com/en-us/dotnet/core/tutorials/with-visual-studio-code?pivots=dotnet-5-0) para criar e executar um projeto "Hello World" no console usando C#. Além disso crie um projeto inicial NUnit usando o comando `dotnet new NUnit`.
<br>Certifique-se de que o arquivo `%appdata%\NuGet\nuget.config` está configurado corretamente, pois alguns desenvolvedores reportaram que estará vazio devido alguns problemas.
Se o arquivo `nuget.config` estiver vazio, ou não configurado corretamente, então o build .NET irá falhar para projetos Selenium.
<br>Adicione a seguinte seção ao arquivo `nuget.config` se ele estiver vazio:
```
<configuration>
  <packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="nuget.org" value="https://www.nuget.org/api/v2/" />   
  </packageSources>
...
```
Para mais informações sobre o arquivo `nuget.config` [clique aqui](https://docs.microsoft.com/en-us/nuget/reference/nuget-config-file).
Você pode ter de personalizar o arquivo `nuget.config` atender suas necessidades.

Agora, volte ao VSCode, pressione Ctrl-Shift-P e digite "NuGet Add Package" e adicione os pacotes requeridos para Selenium, como o pacote `Selenium.WebDriver`. Pressione enter e selecione a versão.
Agora você pode utilizar os exemplos na documentação relacionada para C# com VSCode.

  {{< /tab >}}
  {{< tab header="Ruby" >}}
  A instalação de bibliotecas Selenium para Ruby pode ser feita usando gem:

```shell
gem install selenium-webdriver
```

  {{< /tab >}}
  {{< tab header="JavaScript" >}}
  A instalação de bibliotecas Selenium para JavaScript pode ser feita usando npm:

```shell
npm install selenium-webdriver
```

  {{< /tab >}}
  {{< tab header="Kotlin" >}}
  Devido à ausência de vínculos de linguagem nativo para Kotlin, você deve usar vínculos Java, por exemplo, com Maven [Java](#java)
  {{< /tab >}}
{{< /tabpane >}}

## Próximo passo
[Instale os drivers do navegador]({{< ref "install_drivers.md" >}})
