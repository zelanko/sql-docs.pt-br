---
title: Bancos de dados de desenvolvimento, teste e produção | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- production databases [SQL Server]
- testing databases
- database testing [SQL Server]
ms.assetid: cb403330-8cbe-41c6-bd23-bc432d50f173
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 072f7d671f12335928984d4cebfe57f5bbfe6468
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33047273"
---
# <a name="development-test-and-production-databases-visual-database-tools"></a>Bancos de dados de desenvolvimento, teste e produção (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Se você tiver dois bancos de dados com estruturas idênticas, poderá fazer alterações em um banco de dados e propagá-las para o outro. Por exemplo, se você tiver um banco de dados de desenvolvimento pessoal e um banco de dados de teste para todo o grupo, poderá modificar o banco de dados de desenvolvimento e depois propagar essas alterações para o banco de dados de teste.  
  
Para fazer isso, execute todas as modificações em uma única sessão com o banco de dados de desenvolvimento, crie um Script Change de sua sessão e depois execute o script no banco de dados de teste.  
  
## <a name="see-also"></a>Consulte Também  
[Ambientes multiusuários &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
