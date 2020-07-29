---
title: Bancos de dados de desenvolvimento, teste e produção
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- production databases [SQL Server]
- testing databases
- database testing [SQL Server]
ms.assetid: cb403330-8cbe-41c6-bd23-bc432d50f173
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: e0f50cc149c592633969c84a8f541239d55f1240
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85986746"
---
# <a name="development-test-and-production-databases-visual-database-tools"></a>Bancos de dados de desenvolvimento, teste e produção (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Se você tiver dois bancos de dados com estruturas idênticas, poderá fazer alterações em um banco de dados e propagá-las para o outro. Por exemplo, se você tiver um banco de dados de desenvolvimento pessoal e um banco de dados de teste para todo o grupo, poderá modificar o banco de dados de desenvolvimento e depois propagar essas alterações para o banco de dados de teste.  
  
Para fazer isso, execute todas as modificações em uma única sessão com o banco de dados de desenvolvimento, crie um Script Change de sua sessão e depois execute o script no banco de dados de teste.  
  
## <a name="see-also"></a>Consulte Também  
[Ambientes multiusuários &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
