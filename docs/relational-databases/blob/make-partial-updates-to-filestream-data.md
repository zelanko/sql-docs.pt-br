---
title: Fazer atualizações parciais em dados FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4711a43b544a16f397e07103cd1e8062064396e
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65094270"
---
# <a name="make-partial-updates-to-filestream-data"></a>Fazer atualizações parciais em dados do FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Um aplicativo usa FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT para fazer atualizações parciais em dados de BLOB FILESTREAM. A função [DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527) passa esse valor e o identificador que é retornado de [OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) para o driver FILESTREAM. O driver então força uma cópia de servidor dos dados de FILESTREAM atuais no arquivo referenciado pelo identificador. Se o aplicativo emite o valor FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT depois que o identificador ter sido gravado, a última operação de gravação permanecerá e as operações de gravação anteriores feitas no identificador serão perdidas.  
  
> [!NOTE]  
>  FILESTREAM usa o [protocolo SMB](https://go.microsoft.com/fwlink/?LinkId=112454) para acesso remoto.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o valor `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` para executar uma atualização parcial de um BLOB FILESTREAM inserido.  
  
> [!NOTE]  
>  Este exemplo requer o banco de dados e a tabela habilitados para FILESTREAM criados em [Criar um banco de dados habilitado para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md) e [Como criar uma tabela para armazenar dados de FILESTREAM](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md).  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../relational-databases/blob/codesnippet/cpp/make-partial-updates-to-_1.cpp)]  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar dados do FILESTREAM com OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Criar aplicativos clientes para dados FILESTREAM](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
  
  
