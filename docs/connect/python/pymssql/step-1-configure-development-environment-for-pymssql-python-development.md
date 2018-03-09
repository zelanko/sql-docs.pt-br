---
title: 'Etapa 1: Configurar o ambiente de desenvolvimento do Python pymssql | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: python
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 91916f56a4bbdad46c7fc391257c4575886c28dc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para pymssql desenvolvimento do Python
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o Driver do Python para o SQL Server.    
  
Observe que os Drivers de SQL do Python usa o protocolo TDS, que é habilitado por padrão no SQL Server e banco de dados do SQL Azure.  Nenhuma configuração adicional é necessária.  
  
## <a name="windows"></a>Windows  
  
1. **Instalar o tempo de execução do Python e pip Gerenciador de pacotes**  
a. Vá para [python.org](https://www.python.org/downloads/)  
b. Clique no link apropriado Windows instalador msi.   
c. Executar uma vez baixado o msi para instalar o tempo de execução do Python  
  
2. **Baixar o módulo pymssql** de [aqui](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Verifique se que você escolher o arquivo whl correto.  Por exemplo: escolha se você estiver usando o Python 2.7 em um computador de 64 bits: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Após baixar o arquivo .whl colocá-lo a pasta c: / Python27.  
      
3. **Abrir cmd.exe**  
  
4. **Instalar o módulo pymssql**     
    Por exemplo, se você estiver usando o Python 2.7 em um computador de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instalar o tempo de execução do Python e Gerenciador de pacotes de pip** Python vem pré-instalado na maioria das distribuições do Ubuntu.  Se seu computador não tiver python instalado, você pode obter o download do tarball da fonte de [python.org](https://www.python.org/downloads/) e criar localmente, ou você pode usar o Gerenciador de pacotes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abra terminal**  
  
3.  **Install pymssql module e dependências**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalar o tempo de execução do Python e pip Gerenciador de pacotes**  
a. Vá para [python.org](https://www.python.org/downloads/)  
b. Clique no link apropriado Mac instalador pkg.   
c. Executar uma vez baixado o pacote para instalar o tempo de execução do Python  
  
2.  **Abra terminal**  
  
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
