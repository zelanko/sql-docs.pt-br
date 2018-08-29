---
title: 'Usando as anotações SQL: Identity e SQL: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 33bc05d0161caa2dacdc42a86f0255775fe69e79
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058258"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Usando as anotações sql:identity e sql:guid
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode especificar o **: Identity** e **SQL: GUID** anotações em um esquema XSD em qualquer nó que é mapeado para uma coluna de banco de dados na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Enquanto o formato do diagrama de atualização oferece suporte a **updg: em identidade** e **updg: GUID** atributos, o formato DiffGram não faz isso. O **updg: em identidade** atributo define o comportamento ao atualizar uma coluna de tipo de identidade. O **updg: GUID** atributo permite que você obtenha um valor GUID da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usá-lo no diagrama de atualização. Para obter mais informações e exemplos de funcionamento, consulte [inserindo dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 O **: Identity** e **SQL: GUID** anotações estendem essa funcionalidade a DiffGrams.  
  
 Quando você executa um DiffGram, ele é primeiro convertido em um diagrama de atualização e, em seguida, o diagrama de atualização é executado. Especificando o **: Identity** e **SQL: GUID** anotações no esquema XSD, você está na verdade definindo o comportamento de um diagrama de atualização. Assim, todas as anotações são descritas no contexto de um diagrama de atualização. As anotações podem ser usadas para DiffGrams e diagramas de atualização; entretanto, os diagramas de atualização já fornecem um modo mais avançado de tratar valores de GUID e identidade.  
  
 O **: Identity** e **SQL: GUID** anotações podem ser definidas em um elemento de conteúdo complexo.  
  
## <a name="sqlidentity-annotation"></a>Anotação sql:identity  
 Você pode especificar o **: Identity** anotação no esquema XSD em qualquer nó que mapeia para uma coluna de banco de dados do tipo de identidade. O valor especificado para esta anotação define como a coluna do tipo IDENTITY é atualizada (usando o valor fornecido no diagrama de atualização para modificar a coluna ou ignorando o valor; nesse caso, um valor gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado para esta coluna).  
  
 O **: Identity** anotação pode ser atribuída a dois valores:  
  
 ignore  
 Direciona o diagrama de atualização para ignorar qualquer valor que seja fornecido no diagrama de atualização para essa coluna e para depender do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar o valor da identidade.  
  
 useValue  
 Direciona o diagrama de atualização para usar o valor que é fornecido no diagrama de atualização para atualizar a coluna do tipo IDENTITY. Um diagrama de atualização não verifica se a coluna é um valor de identidade ou não.  
  
 Se o diagrama Especifica um valor para a coluna de tipo de identidade, o **: Identity = "useValue"** deve ser especificado no esquema.  
  
## <a name="sqlguid-annotation"></a>Anotação sql:guid  
 Um diagrama de atualização pode fazer o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerar um valor de GUID e então usar esse valor no diagrama de atualização. No contexto de DiffGrams, você pode usar o **SQL: GUID** anotação para especificar se deseja usar um valor GUID que é gerado pelo SQL Server ou usar o valor que é fornecido no diagrama de atualização para essa coluna.  
  
 O **SQL: GUID** anotação pode ser atribuída a dois valores:  
  
 generate  
 Especifica que o GUID gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja usado para essa coluna na operação de atualização.  
  
 useValue  
 Especifica que o valor especificado no diagrama de atualização seja usado para a coluna. Este é o valor padrão.  
  
  
