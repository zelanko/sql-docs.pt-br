---
title: 'Etapa 1: Configurar o ambiente de desenvolvimento do Python pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: beb0c34f5645615a69944088163ad157d59d3c3a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para pyodbc desenvolvimento do Python

## <a name="windows"></a>Windows  
Conecte-se ao banco de dados SQL usando Python - pyodbc no Windows:
  
1. **Baixar o instalador do Python**  
  Se seu computador não tiver Python instale-o. Acesse o [página de download do Python](https://www.python.org/downloads/windows/) e baixar o instalador apropriado. Por exemplo, se você estiver usando um computador de 64 bits, baixe o instalador de Python 2.7 ou 3.5 (x64).  
  
2. **Instalar o Python** depois que o instalador é baixado, faça o seguinte: uma. Clique duas vezes no arquivo para iniciar o instalador. B. Selecione seu idioma e concordar com os termos. c. Siga as instruções na tela e Python deve ser instalado em seu computador. d. Você pode verificar que é Python é instalado, vá para C:\Python27 ou C:\Python35 e execute o python - v ou piar - v (para 3. x) 
      
3. [**Instalar o Driver ODBC da Microsoft**](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)
  
4. **Abrir cmd.exe como administrador.**     

5. **Instalar o pyodbc usando pip - Python package manager**
```  
> cd C:\Python27\Scripts>  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conecte-se ao banco de dados SQL usando Python - pyodbc no Ubuntu e RedHat:
  
1. **Abra terminal**  

2. **Instalar o Microsoft ODBC Driver 13 para Linux** para Ubuntu 15.04 + 
``` 
> sudo su  
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-Ubuntu-b87369f0/file/154097/2/installodbc.sh  
> sh installodbc.sh  
```   

  Para RedHat 6,7 
``` 
> sudo su 
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-SQL-8d067754/file/153653/4/install.sh 
> sh install.sh 
```  
  
3.  **Instalar pyodbc**  
```  
> sudo -H pip install pyodbc
```
