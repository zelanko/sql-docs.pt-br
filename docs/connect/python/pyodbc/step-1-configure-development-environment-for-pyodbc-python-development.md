---
title: 'Etapa 1: Configurar o ambiente de desenvolvimento Python pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f588174ea80677066628cb3e756d7c38bd42fba
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2018
ms.locfileid: "42784511"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento Python pyodbc

## <a name="windows"></a>Windows  
Conectar-se ao banco de dados SQL usando Python – pyodbc no Windows:
  
1. **Baixe o instalador do Python**.  
  Se seu computador não tiver o Python, instalá-lo. Vá para o [página de download do Python](https://www.python.org/downloads/windows/) e baixar o instalador apropriado. Por exemplo, se você estiver em um computador de 64 bits, baixe o instalador do Python 2.7 ou 3.7 (x64).  
  
2. **Instalar o Python**.  Depois que o instalador for baixado, execute as seguintes etapas: um. Clique duas vezes no arquivo para iniciar o instalador. B. Selecione seu idioma e concordar com os termos. c. Siga as instruções na tela e Python deve ser instalados em seu computador. d. Você pode verificar se o Python está instalado, vá para `C:\Python27` ou `C:\Python37` e execute `python -V` ou `py -V` (para 3. x) 
      
3. [**Bem-vindo ao Microsoft ODBC Driver for SQL Server no Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Abrir cmd.exe como administrador.**     

5. **Instale o pyodbc usando pip - Gerenciador de pacotes do Python** (substitua `C:\Python27\Scripts` com seu caminho do Python instalado)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conectar-se ao banco de dados SQL usando Python – pyodbc:
  
1. **Abrir terminal**  

2. [**Microsoft ODBC Driver for SQL Server no Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Instalar pyodbc**  
```  
> sudo -H pip install pyodbc
```
