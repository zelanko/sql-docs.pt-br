---
title: 'Etapa 1: configurar o ambiente de desenvolvimento pymssql Python | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bf2942b79cf7e72efbb36a53019de8208cd3b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935823"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Etapa 1: configurar o ambiente de desenvolvimento para o desenvolvimento Python pymssql
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o driver Python para SQL Server.    
  
Observe que os drivers do Python SQL usam o protocolo TDS, que é habilitado por padrão no SQL Server e no banco de dados SQL do Azure.  Nenhuma configuração adicional é necessária.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar o tempo de execução do Python e o Gerenciador de pacotes Pip**  
A. Vá para [Python.org](https://www.python.org/downloads/)  
B. Clique no link MSI apropriado do Windows Installer.   
c. Depois de baixado, execute o MSI para instalar o tempo de execução do Python  
  
2. **Baixe o módulo pymssql** [aqui](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Certifique-se de escolher o arquivo WHL correto.  Por exemplo: se você estiver usando o Python 2,7 em um computador de 64 bits, escolha: pymssql-2.1.1-cp27-None-win_amd64. WHL. Depois de baixar o arquivo. WHL, coloque-o na pasta C:/Python27.  
      
3. **Abrir cmd. exe**  
  
4. **Instalar o módulo pymssql**     
    Por exemplo, se você estiver usando o Python 2,7 em um computador de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instalar o tempo de execução do Python e o Gerenciador de pacotes Pip**  O Python vem pré-instalado na maioria das distribuições do Ubuntu.  Se seu computador não tiver o Python instalado, você poderá baixar o tarball de origem do [Python.org](https://www.python.org/downloads/) e criar localmente, ou pode usar o Gerenciador de pacotes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abrir terminal**  
  
3.  **Instalar o módulo e as dependências do pymssql**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar o tempo de execução do Python e o Gerenciador de pacotes Pip**  
A. Vá para [Python.org](https://www.python.org/downloads/)  
B. Clique no link do pacote do Mac Installer apropriado.   
c. Depois de baixado, execute o pacote para instalar o tempo de execução do Python  
  
2.  **Abrir terminal**  
  
3. **Instalar o Gerenciador de pacotes do Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Instalar o módulo FreeTDS**  
```  
> brew install FreeTDS  
```  
  
5.  **Instalar o módulo pymssql**  
```  
> sudo -H pip install pymssql  
```
