---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: edcba0cfc8ca284fd046f787829af4ba73dd366b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121914"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  Melhorias no início de mecanismo de banco de dados com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir ICommandWithParameters:: Getparameterinfo obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por CommandWithParameters::GetParameterInfo nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
 Também a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ao chamar ICommandWithParameters:: SetParameterInfo, o valor passado para o *pwszName* parâmetro deve ser um identificador válido. Para obter mais informações, consulte [Database Identifiers](../databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  