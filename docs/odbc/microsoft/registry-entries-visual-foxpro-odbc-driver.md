---
title: Entradas de registro (Visual FoxPro ODBC Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd2d419a94c45a872789e095b014159b41d7c217
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304833"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas do Registro (Driver ODBC do Visual FoxPro)
Quando você instala o Visual FoxPro ODBC Driver, o programa de instalação atualiza o registro do sistema, na chave de registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, para adicionar uma nova chave chamada Microsoft Visual FoxPro Driver. Sob essa tecla, são adicionados os valores descritos na tabela a seguir.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|Funções de conexão|REG_SZ|"YYN"|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc.dll|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUse|REG_SZ|"1"|  
|Instalação|REG_SZ|Caminho do sistema para o arquivo vfpodbc.dll|  
|SQLLevel|REG_SZ|"0"|  
  
 O programa de instalação também adiciona a chave "Visual FoxPro Files", representando o driver Visual FoxPro padrão, à chave HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini. Nesta tecla, o programa de instalação adiciona os valores descritos na tabela a seguir.  
  
|Nome do valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc.dll|  
  
 Cada vez que você adiciona uma fonte de dados Visual FoxPro ODBC à sua configuração ODBC, uma nova chave é adicionada para esse nome de origem de dados. Os valores para a fonte de dados correspondem aos valores definidos na caixa de diálogo **Configuração Visual FoxPro do ODBC,** conforme listado na tabela a seguir.  
  
|Nome de valor (palavra-chave)|Tipo de valor|Valor|  
|----------------------------|----------------|-----------|  
|Agrupar|REG_SQ|Qualquer seqüência de colagem suportada|  
|Descrição|REG_SZ|Descrição do usuário da fonte de dados|  
|Driver||Caminho do sistema para o arquivo vfpodbc.dll|  
|Exclusivo||Sim ou não|  
|Busca de fundo||Sim ou não|  
|SourceDB|REG_SZ|Caminho para . Arquivo DBC|  
|SourceType|REG_SZ|"DBC" ou "DBF"|  
  
 Você não deve acessar essas informações diretamente; qualquer administração do registro é tratada pelo administrador do ODBC quando você adiciona, modifica ou exclui uma fonte de dados.  
  
 Você pode usar algumas dessas palavras-chave e valores como parâmetros na função [API SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC.
