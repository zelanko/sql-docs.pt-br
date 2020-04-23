---
title: 'Etapa 1: configurar o ambiente de desenvolvimento para o Node.js'
description: Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolvimento um aplicativo usando o Driver do Node.js para SQL Server.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38337772d9ec9db2503637122d0d1b616dc6ef5f
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528130"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Etapa 1:  Configurar o ambiente de desenvolvimento para o desenvolvimento de Node.js
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolvimento um aplicativo usando o Driver do Node.js para SQL Server.  O método mais comum é usar o npm (gerenciador de pacotes de nó) para instalar o módulo tedious, mas você poderá baixar esse módulo diretamente do [GitHub](https://github.com/pekim/tedious), se preferir.  
  
O driver do Node.js usa o protocolo TDS, que é habilitado por padrão no SQL Server e no Banco de Dados SQL do Azure.  É necessário realizar uma configuração adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instale o runtime do Node.js e o gerenciador de pacotes npm.**  
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
  
5. **Instale um módulo tedious em seu projeto.**  Tedious é a implementação do protocolo TDS usada para se comunicar com o SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Abra o terminal**  
  
2. **Instale o runtime do Node.js.**  
```  
>sudo apt-get install node  
```  
3. **Instale o npm (gerenciador de pacotes de nó).**  
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
  
6. **Instale um módulo tedious em seu projeto.**  Tedious é a implementação do protocolo TDS usada para se comunicar com o SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="macos"></a>macOS  
  
1. **Instale o runtime do Node.js e o gerenciador de pacotes npm.**  
a. Vá para [Node.js](https://nodejs.org/en/download/)  
b. Clique no link do instalador do macOS apropriado.  
c. Depois de baixado, execute o "dmg" para instalar o Node.js  
  
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
