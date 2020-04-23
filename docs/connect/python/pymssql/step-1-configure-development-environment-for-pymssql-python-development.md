---
title: 'Etapa 1: Configurar o ambiente pymssql'
description: A etapa 1 deste guia de introdução envolve a instalação do Python, do Microsoft ODBC Driver for SQL Server e do pymssql em seu ambiente de desenvolvimento.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5eb4a746cf8847c8300091677fe4e07e8173707
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634609"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento Python pymssql
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolvimento um aplicativo usando o Driver do Python para SQL Server.    
  
Os Drivers SQL do Python usam o protocolo TDS, que está habilitado por padrão no SQL Server e no Banco de Dados SQL do Azure.  É necessário realizar uma configuração adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar o runtime do Python e o gerenciador de pacotes pip.**  
a. Acesse [python.org](https://www.python.org/downloads/)  
b. Clique no link MSI apropriado do Windows Installer.   
c. Depois de baixado, execute o msi para instalar o runtime do Python  
  
2. **Baixe o módulo pymssql** [aqui](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Verifique se você escolheu o arquivo `whl` correto.  Por exemplo:  Se você estiver usando o Python 2.7 em um computador de 64 bits, escolha `pymssql‑2.1.1‑cp27‑none‑win_amd64.whl`. Depois de baixar o arquivo `whl`, coloque-o na pasta C:\Python27.  
      
3. **Abra cmd.exe**  
  
4. **Instale o módulo pymssql.**  
    Por exemplo, se você estiver usando o Python 2.7 em um computador de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instale o runtime do Python e o gerenciador de pacotes pip.**  O Python vem pré-instalado na maioria das distribuições do Ubuntu.  Se o computador não tiver o Python instalado, você poderá baixar o tarball de origem em [python.org](https://www.python.org/downloads/) e compilar localmente ou poderá usar o gerenciador de pacotes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abra o terminal**  
  
3.  **Instale o módulo e as dependências do pymssql**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="macos"></a>macOS
  
1. **Instalar o runtime do Python e o gerenciador de pacotes pip**  
a. Acesse [python.org](https://www.python.org/downloads/)  
b. Clique no link pkg do instalador do macOS apropriado.   
c. Depois de baixado, execute o pkg para instalar o runtime do Python  
  
2.  **Abra o terminal**  
  
3. **Instale o gerenciador de pacotes do Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Instale o módulo FreeTDS**  
```  
> brew install FreeTDS  
```  
  
5.  **Instale o módulo pymssql**  
```  
> sudo -H pip install pymssql  
```
