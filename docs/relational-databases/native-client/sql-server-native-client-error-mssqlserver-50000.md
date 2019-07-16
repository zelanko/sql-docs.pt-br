---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63431d2f8f20159d65a02833c2f24e08d180321a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031734"
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
  
