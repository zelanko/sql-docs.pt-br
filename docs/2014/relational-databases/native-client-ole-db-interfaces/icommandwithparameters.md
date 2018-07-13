---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c43b41faa03ae9838cc0dcec619179d272f238e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408146"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  Melhorias no início de mecanismo de banco de dados com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir ICommandWithParameters:: Getparameterinfo Obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters::GetParameterInfo nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
 Além da partir [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ao chamar ICommandWithParameters:: SetParameterInfo, o valor passado para o *pwszName* parâmetro deve ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
