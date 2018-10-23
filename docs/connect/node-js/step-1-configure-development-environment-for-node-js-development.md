---
title: 'Etapa 1: configurar o ambiente de desenvolvimento para o desenvolvimento de Node.js | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 823177f8fef91dda8cf879f6be84ef6706224fad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600234"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Etapa 1: configurar o ambiente de desenvolvimento para o desenvolvimento de Node.js
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o Driver do Node. js para SQL Server.  O método mais comum é usar o node package manager (npm) para instalar o módulo entediante, mas você pode baixar o módulo entediante diretamente no [Github](https://github.com/pekim/tedious) se você preferir.  
  
Observe que o Driver do Node. js usa o protocolo TDS, que é habilitado por padrão no SQL Server e banco de dados SQL.  Nenhuma configuração adicional é necessária.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar o Gerenciador de pacotes de tempo de execução e o npm do Node. js**  
A. Vá para [Node. js](https://nodejs.org/en/download/)  
B. Clique no link apropriado Windows instalador msi.   
c. Após o download, execute o msi para instalar o Node. js  
  
2. **Abra cmd.exe**  
  
3. **Crie um diretório de projeto** e navegue até ele.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Crie um projeto de nó.**  Para manter os padrões durante a criação de seu projeto, pressione enter até que o projeto é criado. No final desta etapa, você deverá ver um arquivo Package. JSON no diretório do projeto.  
```  
> npm init  
```  
  
5. **Instale o módulo entediante em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abrir terminal**  
  
2. **Instalar o tempo de execução do Node. js**  
```  
>sudo apt-get install node  
```  
3. **Instale o npm (Gerenciador de pacotes do nó)**  
```  
> sudo apt-get install npm  
```  
4. **Crie um diretório de projeto** e navegue até ele.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Crie um projeto de nó.**  Para manter os padrões durante a criação de seu projeto, pressione enter até que o projeto é criado. No final desta etapa, você deverá ver um arquivo Package. JSON no diretório do projeto.  
```  
> sudo npm init  
```  
  
6. **Instale o módulo entediante em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar o Gerenciador de pacotes de tempo de execução e o npm do Node. js**  
A. Vá para [Node. js](https://nodejs.org/en/download/)  
B. Clique no link apropriado de instalador do Mac OS.  
c. Após o download, execute o dmg para instalar o Node. js  
  
2. **Abrir terminal**  
  
3. **Crie um diretório de projeto** e navegue até ele.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Crie um projeto de nó.**  Para manter os padrões durante a criação de seu projeto, pressione enter até que o projeto é criado. No final desta etapa, você deverá ver um arquivo Package. JSON no diretório do projeto.  
```  
> npm init  
```  
  
5. **Instale o módulo entediante em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> npm install tedious  
```  
  
