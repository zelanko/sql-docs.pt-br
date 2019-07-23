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
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003761"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Etapa 1: configurar o ambiente de desenvolvimento para o desenvolvimento de Node.js
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o driver node. js para SQL Server.  O método mais comum é usar o Gerenciador de pacotes de nó (NPM) para instalar o módulo entediante, mas você pode baixar o módulo entediante diretamente no [GitHub](https://github.com/pekim/tedious) , se preferir.  
  
Observe que o driver node. js usa o protocolo TDS, que é habilitado por padrão no SQL Server e no banco de dados SQL do Azure.  Nenhuma configuração adicional é necessária.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar o tempo de execução do node. js e o Gerenciador de pacotes NPM**  
A. Vá para [node. js](https://nodejs.org/en/download/)  
B. Clique no link MSI apropriado do Windows Installer.   
c. Depois de baixado, execute o MSI para instalar o Node. js  
  
2. **Abrir cmd. exe**  
  
3. **Crie um diretório do projeto** e navegue até ele.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Crie um projeto de nó.**  Para manter os padrões durante a criação do projeto, pressione ENTER até que o projeto seja criado. No final desta etapa, você deverá ver um arquivo Package. JSON no diretório do projeto.  
```  
> npm init  
```  
  
5. **Instale um módulo entediante em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abrir terminal**  
  
2. **Instalar o tempo de execução do node. js**  
```  
>sudo apt-get install node  
```  
3. **Instalar o NPM (Gerenciador de pacotes do nó)**  
```  
> sudo apt-get install npm  
```  
4. **Crie um diretório do projeto** e navegue até ele.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Crie um projeto de nó.**  Para manter os padrões durante a criação do projeto, pressione ENTER até que o projeto seja criado. No final desta etapa, você deverá ver um arquivo Package. JSON no diretório do projeto.  
```  
> sudo npm init  
```  
  
6. **Instale um módulo entediante em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar o tempo de execução do node. js e o Gerenciador de pacotes NPM**  
A. Vá para [node. js](https://nodejs.org/en/download/)  
B. Clique no link Mac OS Installer apropriado.  
c. Depois de baixado, execute o dmg para instalar o Node. js  
  
2. **Abrir terminal**  
  
3. **Crie um diretório do projeto** e navegue até ele.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Crie um projeto de nó.**  Para manter os padrões durante a criação do projeto, pressione ENTER até que o projeto seja criado. No final desta etapa, você deverá ver um arquivo Package. JSON no diretório do projeto.  
```  
> npm init  
```  
  
5. **Instale um módulo entediante em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> npm install tedious  
```  
  
