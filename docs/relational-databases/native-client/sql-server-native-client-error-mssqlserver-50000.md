---
title: MSSQLSERVER_50000 | Microsoft Docs
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9200df4bf60b0eced76bafd0755f4dd8e9a17bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629681"
---
# <a name="sql-server-native-client-error-mssqlserver50000"></a>Erro do SQL Server Native Client MSSQLSERVER_50000
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|Versão do Produto|11.0|  
|ID do evento|50000|  
|Origem do evento|SETUP|  
|Componente|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro de rede ao tentar ler a partir do arquivo '%. * ls'.|  
  
## <a name="explanation"></a>Explicação  
 Foi feita uma tentativa de instalar (ou atualizar) o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client em um computador onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client já foi instalado e onde a instalação existente era de um arquivo MSI que foi renomeado de sqlncli.msi.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver este erro, desinstale a versão existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para evitar esse erro, não instale o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client de um arquivo MSI que não seja denominado sqlncli.msi.  
  
## <a name="internal-only"></a>Somente interno  
  
