---
title: Usando as anotações sql:identity e sql:guid
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50483d7f6f84371b42bf0c79fbc74a1f85a65eab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246816"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Usando as anotações sql:identity e sql:guid
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode especificar as anotações **SQL: Identity** e **SQL: GUID** em um esquema XSD em qualquer nó que seja mapeado para uma coluna de banco [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de dados no. Enquanto o formato updategram dá suporte aos atributos **updg: at-identity** e **updg: GUID** , o formato DiffGram não faz isso. O atributo **updg: at-identity** define o comportamento na atualização de uma coluna de tipo de identidade. O atributo **updg: GUID** permite obter um valor de GUID de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usá-lo no updategram. Para obter mais informações e exemplos de trabalho, consulte [inserindo dados usando UPDATEGRAMS XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 As anotações **SQL: Identity** e **SQL: GUID** estendem essa funcionalidade para DiffGrams.  
  
 Quando você executa um DiffGram, ele é primeiro convertido em um diagrama de atualização e, em seguida, o diagrama de atualização é executado. Ao especificar as anotações **SQL: Identity** e **SQL: GUID** no esquema XSD, você está na verdade definindo o comportamento de um updategram. Assim, todas as anotações são descritas no contexto de um diagrama de atualização. As anotações podem ser usadas para DiffGrams e diagramas de atualização; entretanto, os diagramas de atualização já fornecem um modo mais avançado de tratar valores de GUID e identidade.  
  
 As anotações **SQL: Identity** e **SQL: GUID** podem ser definidas em um elemento de conteúdo complexo.  
  
## <a name="sqlidentity-annotation"></a>Anotação sql:identity  
 Você pode especificar a anotação **SQL: Identity** no esquema XSD em qualquer nó que seja mapeado para uma coluna de banco de dados do tipo identidade. O valor especificado para essa anotação define como a coluna de tipo de identidade é atualizada (usando o valor fornecido no updategram para modificar a coluna ou ignorando o valor; nesse caso, um valor gerado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]por um é usado para essa coluna).  
  
 A anotação **SQL: Identity** pode ser atribuída a dois valores:  
  
 ignore  
 Direciona o diagrama de atualização para ignorar qualquer valor que seja fornecido no diagrama de atualização para essa coluna e para depender do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar o valor da identidade.  
  
 useValue  
 Direciona o diagrama de atualização para usar o valor que é fornecido no diagrama de atualização para atualizar a coluna do tipo IDENTITY. Um diagrama de atualização não verifica se a coluna é um valor de identidade ou não.  
  
 Se o updategram especificar um valor para a coluna de tipo de identidade, o **SQL: Identity = "useValue"** deverá ser especificado no esquema.  
  
## <a name="sqlguid-annotation"></a>Anotação sql:guid  
 Um diagrama de atualização pode fazer o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerar um valor de GUID e então usar esse valor no diagrama de atualização. No contexto de DiffGrams, você pode usar a anotação **SQL: GUID** para especificar se deve usar um valor GUID gerado pelo SQL Server ou usar o valor que é fornecido no updategram para essa coluna.  
  
 A anotação **SQL: GUID** pode ser atribuída a dois valores:  
  
 generate  
 Especifica que o GUID gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja usado para essa coluna na operação de atualização.  
  
 useValue  
 Especifica que o valor especificado no diagrama de atualização seja usado para a coluna. Esse é o valor padrão.  
  
  
