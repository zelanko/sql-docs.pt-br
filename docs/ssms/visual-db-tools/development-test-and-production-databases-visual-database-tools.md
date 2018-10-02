---
title: Bancos de dados de desenvolvimento, teste e produção | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- production databases [SQL Server]
- testing databases
- database testing [SQL Server]
ms.assetid: cb403330-8cbe-41c6-bd23-bc432d50f173
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 214c70d9c71053b81e81b9228bca5b42167eabc5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684204"
---
# <a name="development-test-and-production-databases-visual-database-tools"></a>Bancos de dados de desenvolvimento, teste e produção (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Se você tiver dois bancos de dados com estruturas idênticas, poderá fazer alterações em um banco de dados e propagá-las para o outro. Por exemplo, se você tiver um banco de dados de desenvolvimento pessoal e um banco de dados de teste para todo o grupo, poderá modificar o banco de dados de desenvolvimento e depois propagar essas alterações para o banco de dados de teste.  
  
Para fazer isso, execute todas as modificações em uma única sessão com o banco de dados de desenvolvimento, crie um Script Change de sua sessão e depois execute o script no banco de dados de teste.  
  
## <a name="see-also"></a>Consulte Também  
[Ambientes multiusuários &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
