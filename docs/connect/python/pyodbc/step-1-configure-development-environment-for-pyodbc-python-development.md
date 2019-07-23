---
title: 'Etapa 1: configurar o ambiente de desenvolvimento pyodbc Python | Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a1a43540d866faaf79b1c020eb255689862e6d97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992525"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento Python pyodbc

## <a name="windows"></a>Windows  
Conecte-se ao banco de dados SQL usando Python-pyodbc no Windows:
  
1. **Baixe o instalador do Python**.  
  Se seu computador não tiver o Python, instale-o. Vá para a [página de download do Python](https://www.python.org/downloads/windows/) e baixe o instalador apropriado. Por exemplo, se você estiver em um computador de 64 bits, baixe o instalador do Python 2,7 ou 3,7 (x64).  
  
2. **Instalar o Python**.  Depois que o instalador for baixado, execute as seguintes etapas: a. Clique duas vezes no arquivo para iniciar o instalador. B. Selecione seu idioma e concorde com os termos. c. Siga as instruções na tela e o Python deve ser instalado em seu computador. d. Você pode verificar se o `C:\Python27` Python está instalado acessando ou `C:\Python37` e `python -V` executando `py -V` ou (para 3. x) 
      
3. [**Bem-vindo ao Microsoft ODBC Driver for SQL Server no Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Abrir cmd. exe como administrador**     

5. **Instalar o pyodbc usando o Gerenciador de pacotes Pip-Python** (Substitua `C:\Python27\Scripts` pelo caminho Python instalado)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conecte-se ao banco de dados SQL usando Python-pyodbc:
  
1. **Abrir terminal**  

2. [**Microsoft ODBC Driver for SQL Server no Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Instalar o pyodbc**  
```  
> sudo -H pip install pyodbc
```
