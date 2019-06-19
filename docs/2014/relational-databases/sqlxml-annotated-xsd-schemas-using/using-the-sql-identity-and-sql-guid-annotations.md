---
title: 'Usando as anotações SQL: Identity e SQL: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6135f1b46e9b2312f01b9ff7a7ebdd08d2d34a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013634"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Usando as anotações sql:identity e sql:guid
  Você pode especificar o `sql:identity` e `sql:guid` anotações em um esquema XSD em qualquer nó que mapeia para uma coluna de banco de dados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Enquanto o formato de diagrama de atualização dá suporte aos atributos `updg:at-identity` e `updg:guid`, isso não ocorre com o formato DiffGram. O atributo `updg:at-identity` define o comportamento ao atualizar uma coluna do tipo IDENTITY. O atributo `updg:guid` permite obter um valor de GUID do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o utilizar no diagrama de atualização. Para obter mais informações e exemplos de funcionamento, consulte [inserindo dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 As anotações `sql:identity` e `sql:guid` estendem esta funcionalidade a DiffGrams.  
  
 Quando você executa um DiffGram, ele é primeiro convertido em um diagrama de atualização e, em seguida, o diagrama de atualização é executado. Ao especificar as anotações `sql:identity` e `sql:guid` no esquema XSD, você está na verdade definindo o comportamento de um diagrama de atualização. Assim, todas as anotações são descritas no contexto de um diagrama de atualização. As anotações podem ser usadas para DiffGrams e diagramas de atualização; entretanto, os diagramas de atualização já fornecem um modo mais avançado de tratar valores de GUID e identidade.  
  
 As anotações `sql:identity` e `sql:guid` podem ser definidas em um elemento de conteúdo complexo.  
  
## <a name="sqlidentity-annotation"></a>Anotação sql:identity  
 Você pode especificar a anotação `sql:identity` no esquema XSD em qualquer nó mapeado para uma coluna de banco de dados do tipo IDENTITY. O valor especificado para esta anotação define como a coluna de tipo de identidade é atualizada (usando-se o valor fornecido no diagrama de atualização para modificar a coluna ou ignorando o valor, caso em que um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-valor gerado é usado para esta coluna).  
  
 É possível atribuir dois valores à anotação `sql:identity`:  
  
 ignore  
 Direciona o diagrama de atualização para ignorar qualquer valor que seja fornecido no diagrama de atualização para essa coluna e para depender do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar o valor da identidade.  
  
 useValue  
 Direciona o diagrama de atualização para usar o valor que é fornecido no diagrama de atualização para atualizar a coluna do tipo IDENTITY. Um diagrama de atualização não verifica se a coluna é um valor de identidade ou não.  
  
 Se o diagrama de atualização especificar um valor para a coluna do tipo IDENTITY, `sql:identity="useValue"` deve ser especificado no esquema.  
  
## <a name="sqlguid-annotation"></a>Anotação sql:guid  
 Um diagrama de atualização pode fazer o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerar um valor de GUID e então usar esse valor no diagrama de atualização. No contexto de DiffGrams, você pode usar a anotação `sql:guid` para especificar se deve ser usado um valor de GUID gerado pelo SQL Server ou um valor que é fornecido no diagrama de atualização para essa coluna.  
  
 É possível atribuir dois valores à anotação `sql:guid`:  
  
 generate  
 Especifica que o GUID gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja usado para essa coluna na operação de atualização.  
  
 useValue  
 Especifica que o valor especificado no diagrama de atualização seja usado para a coluna. Este é o valor padrão.  
  
  
