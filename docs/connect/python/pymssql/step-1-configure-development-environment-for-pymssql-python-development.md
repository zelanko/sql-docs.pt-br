---
title: 'Etapa 1: Configurar o ambiente de desenvolvimento Python pymssql | Microsoft Docs'
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
manager: jroth
ms.openlocfilehash: 9d74e3ce2f7db91aca295dcb7507431a82e49c8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803871"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Etapa 1: configurar o ambiente de desenvolvimento para o desenvolvimento Python pymssql
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o Driver Python para SQL Server.    
  
Observe que os Drivers do SQL Python usam o protocolo TDS, que é habilitado por padrão no SQL Server e banco de dados SQL.  Nenhuma configuração adicional é necessária.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar o tempo de execução do Python e o Gerenciador de pacotes do pip**  
A. Vá para [python.org](https://www.python.org/downloads/)  
B. Clique no link apropriado Windows instalador msi.   
c. Executar uma vez baixado o msi para instalar o tempo de execução do Python  
  
2. **Baixar o módulo pymssql** de [aqui](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Verifique se que você escolher o arquivo whl correto.  Por exemplo: se você estiver usando o Python 2.7 em um computador de 64 bits, escolha: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Depois de baixar o arquivo. whl coloque-o na pasta c:/python27.  
      
3. **Abra cmd.exe**  
  
4. **Instalar o módulo pymssql**     
    Por exemplo, se você estiver usando o Python 2.7 em um computador de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instalar o tempo de execução do Python e o Gerenciador de pacotes do pip** Python vem pré-instalado na maioria das distribuições do Ubuntu.  Se seu computador não tiver o python instalado, você pode obter o download do tarball de origem do [python.org](https://www.python.org/downloads/) e criar localmente, ou você pode usar o Gerenciador de pacotes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abrir terminal**  
  
3.  **Instalar o módulo pymssql e dependências**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar o tempo de execução do Python e o Gerenciador de pacotes do pip**  
A. Vá para [python.org](https://www.python.org/downloads/)  
B. Clique no link de pacote do instalador Mac apropriado.   
c. Executar uma vez baixado o pacote para instalar o tempo de execução do Python  
  
2.  **Abrir terminal**  
  
3. **Instalar o Gerenciador de pacotes Homebrew**  
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
