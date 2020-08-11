---
title: MSSQLSERVER_50000 | Microsoft Docs
description: Houve um erro ao tentar instalar ou atualizar o SQL Server Native Client. Veja uma explicação do erro e as possíveis resoluções.
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fbabf983f7866a003b64d8af27c37927b0247dbf
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246548"
---
# <a name="error-mssqlserver_50000-in-sql-server-native-client"></a>Erro MSSQLSERVER_50000 no SQL Server Native Client 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|Versão do produto|11.0|  
|ID do evento|50000|  
|Origem do Evento|SETUP|  
|Componente|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro de rede ao tentar ler a partir do arquivo '%. * ls'.|  
  
## <a name="explanation"></a>Explicação  
 Foi feita uma tentativa de instalar (ou atualizar) o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client em um computador onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client já foi instalado e onde a instalação existente era de um arquivo MSI que foi renomeado de sqlncli.msi.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver este erro, desinstale a versão existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para evitar esse erro, não instale o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client de um arquivo MSI que não seja denominado sqlncli.msi.  
  
## <a name="internal-only"></a>Somente interno  
  
