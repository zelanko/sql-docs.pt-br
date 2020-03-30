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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68003761"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Etapa 1: configurar o ambiente de desenvolvimento para o desenvolvimento de Node.js
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolvimento um aplicativo usando o Driver do Node.js para SQL Server.  O método mais comum é usar o npm (gerenciador de pacotes de nó) para instalar o módulo tedious, mas você poderá baixar o módulo tedious diretamente do [GitHub](https://github.com/pekim/tedious) se preferir.  
  
Observe que o Driver do Node.js usa o protocolo TDS, que é habilitado por padrão no SQL Server e no Banco de Dados SQL do Azure.  É necessário realizar uma configuração adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar o runtime do Node.js e o gerenciador de pacotes npm**  
a. Vá para [Node.js](https://nodejs.org/en/download/)  
b. Clique no link MSI apropriado do Windows Installer.   
c. Depois de baixado, execute o MSI para instalar o Node.js  
  
2. **Abra cmd.exe**  
  
3. **Crie um diretório do projeto** e acesse-o.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Crie um projeto do Node.**  Para manter os padrões durante a criação do projeto, pressione enter até que o projeto seja criado. No final desta etapa, você deverá ver um arquivo package.json no diretório do projeto.  
```  
> npm init  
```  
  
5. **Instale um módulo tedious em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abra o terminal**  
  
2. **Instale o runtime do Node.js**  
```  
>sudo apt-get install node  
```  
3. **Instale o npm (gerenciador de pacotes do nó)**  
```  
> sudo apt-get install npm  
```  
4. **Crie um diretório do projeto** e acesse-o.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Crie um projeto do Node.**  Para manter os padrões durante a criação do projeto, pressione enter até que o projeto seja criado. No final desta etapa, você deverá ver um arquivo package.json no diretório do projeto.  
```  
> sudo npm init  
```  
  
6. **Instale um módulo tedious em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar o runtime do Node.js e o gerenciador de pacotes npm**  
a. Vá para [Node.js](https://nodejs.org/en/download/)  
b. Clique no link do instalador do Mac OS apropriado.  
c. Depois de baixado, execute o dmg para instalar o Node.js  
  
2. **Abra o terminal**  
  
3. **Crie um diretório do projeto** e acesse-o.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Crie um projeto do Node.**  Para manter os padrões durante a criação do projeto, pressione enter até que o projeto seja criado. No final desta etapa, você deverá ver um arquivo package.json no diretório do projeto.  
```  
> npm init  
```  
  
5. **Instale um módulo tedious em seu projeto.**  Esta é a implementação do protocolo TDS que o driver usa para se comunicar com o SQL Server.  
```  
> npm install tedious  
```  
  
