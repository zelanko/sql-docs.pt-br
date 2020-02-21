---
title: 'Etapa 1: Configurar ambiente de desenvolvimento pyodbc Python| Microsoft Docs'
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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67992525"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento Python pyodbc

## <a name="windows"></a>Windows  
Conecte-se ao Banco de Dados SQL usando Phyton – pyodbc no Windows:
  
1. **Baixe o instalador do Python**.  
  Se seu computador não tiver o Python, instale-o. Acesse a [página de download do Python](https://www.python.org/downloads/windows/) e baixe o instalador apropriado. Por exemplo, se seu computador tem 64 bits, baixe o instalador do Python 2.7 ou 3.7 (x64).  
  
2. **Instalar o Python**.  Depois de baixar o instalador, execute as seguintes etapas: a. Clique duas vezes no arquivo para iniciar o instalador. b. Selecione seu idioma e concorde com os termos. c. Siga as instruções na tela. Pronto, o Python já deve estar instalado no seu computador. d. Para verificar se o Python está instalado, vá para `C:\Python27` ou `C:\Python37` e execute `python -V` ou `py -V` (para 3.x) 
      
3. [**Bem-vindo ao Microsoft ODBC Driver for SQL Server no Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Abra o cmd.exe como administrador**     

5. **Instale o pyodbc usando o gerenciador de pacotes pip – Python** (substitua `C:\Python27\Scripts` pelo caminho do Python instalado)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conecte-se ao Banco de Dados SQL usando Python – pyodbc:
  
1. **Abra o Terminal**  

2. [**Microsoft ODBC Driver for SQL Server no Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Instale o pyodbc**  
```  
> sudo -H pip install pyodbc
```
