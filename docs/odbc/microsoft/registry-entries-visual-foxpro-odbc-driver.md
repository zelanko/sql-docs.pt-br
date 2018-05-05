---
title: Entradas do registro (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a8a742aeb4f2290ef7f76410d689e15afec5c6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas do registro (Driver ODBC do Visual FoxPro)
Quando você instala o Driver de ODBC do Visual FoxPro, o programa de instalação atualiza o registro do sistema, na chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, para adicionar uma nova chave chamada Microsoft Visual FoxPro Driver. Sob essa chave, valores descritos na tabela a seguir são adicionados.  
  
|Nome do valor|Tipo de valor|Value|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|Instalação|REG_SZ|Caminho do sistema para o arquivo vfpodbc|  
|SQLLevel|REG_SZ|"0"|  
  
 O programa de instalação também adiciona a chave "Visual FoxPro arquivos", que representa o driver do Visual FoxPro padrão, a chave de HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini do sistema. Sob essa chave, o programa de instalação adiciona os valores descritos na tabela a seguir.  
  
|Nome do valor|Tipo de valor|Value|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Caminho do sistema para o arquivo vfpodbc|  
  
 Cada vez que você adicionar uma fonte de dados do Visual FoxPro ODBC para sua configuração de ODBC, uma nova chave é adicionada para esse nome de fonte de dados. Os valores da fonte de dados correspondem aos valores definidos no **a instalação do Visual FoxPro ODBC** caixa de diálogo, conforme listado na tabela a seguir.  
  
|Nome do valor (palavra-chave)|Tipo de valor|Value|  
|----------------------------|----------------|-----------|  
|Agrupar|REG_SQ|Nenhum suporte para a sequência de agrupamento|  
|Description|REG_SZ|Descrição da fonte de dados do usuário|  
|Driver||Caminho do sistema para o arquivo vfpodbc|  
|Exclusive||Sim ou Não|  
|BackgroundFetch||Sim ou Não|  
|SourceDB|REG_SZ|Caminho. Arquivo DBC|  
|SourceType|REG_SZ|"DBC" ou "DBF"|  
  
 Você não deve acessar essas informações diretamente. qualquer administração do registro é tratada pelo administrador de ODBC quando você adicionar, modificar ou excluir uma fonte de dados.  
  
 Você pode usar algumas dessas palavras-chave e valores como parâmetros de [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) função da API do ODBC.
