---
title: Fazer atualizações parciais em dados FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cce625b931fda4e70ad67c6e5940c93604c81776
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920087"
---
# <a name="make-partial-updates-to-filestream-data"></a>Fazer atualizações parciais em dados do FILESTREAM
  Um aplicativo usa FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT para fazer atualizações parciais em dados de BLOB FILESTREAM. A função [DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527) passa esse valor e o identificador que é retornado de [OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) para o driver FILESTREAM. O driver então força uma cópia de servidor dos dados de FILESTREAM atuais no arquivo referenciado pelo identificador. Se o aplicativo emite o valor FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT depois que o identificador ter sido gravado, a última operação de gravação permanecerá e as operações de gravação anteriores feitas no identificador serão perdidas.  
  
> [!NOTE]  
>  FILESTREAM usa o [protocolo SMB](https://go.microsoft.com/fwlink/?LinkId=112454) para acesso remoto.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o valor `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` para executar uma atualização parcial de um BLOB FILESTREAM inserido.  
  
> [!NOTE]  
>  Este exemplo requer o banco de dados e a tabela habilitados para FILESTREAM criados em [Criar um banco de dados habilitado para FILESTREAM](create-a-filestream-enabled-database.md) e [Como criar uma tabela para armazenar dados de FILESTREAM](create-a-table-for-storing-filestream-data.md).  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_fsctl)]  
  
## <a name="see-also"></a>Consulte também  
 [Acessar dados do FILESTREAM com OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md)   
 [Criar aplicativos clientes para dados FILESTREAM](create-client-applications-for-filestream-data.md)  
  
  
