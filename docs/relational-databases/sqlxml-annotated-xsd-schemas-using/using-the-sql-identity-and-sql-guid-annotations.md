---
title: Usando as anotações sql:identity e sql:guid
description: Aprenda a usar as anotações sql:identity e sql:guid em um esquema XSD para definir o comportamento de um updategram XML.
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
ms.openlocfilehash: f581c1a5c0d925d48df5a16d95cdb141e2d48f83
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388104"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Usando as anotações sql:identity e sql:guid
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode especificar as anotações **sql:identity** e **sql:guid** em um esquema XSD em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]qualquer nó que mapeie uma coluna de banco de dados em . Considerando que o formato updategram suporta os atributos **updg:at-identity** e **updg:guid,** o formato DiffGram não. O atributo **updg:at-identity** define o comportamento na atualização de uma coluna do tipo IDENTIDADE. O atributo **updg:guid** permite obter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um valor GUID e usá-lo no updategram. Para obter mais informações e amostras de trabalho, consulte [Inserindo dados usando xml updategrams &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 As anotações **sql:identity** e **sql:guid** estendem essa funcionalidade para DiffGrams.  
  
 Quando você executa um DiffGram, ele é primeiro convertido em um diagrama de atualização e, em seguida, o diagrama de atualização é executado. Ao especificar as anotações **sql:identity** e **sql:guid** no esquema XSD, você está de fato definindo o comportamento de um updategram. Assim, todas as anotações são descritas no contexto de um diagrama de atualização. As anotações podem ser usadas para DiffGrams e diagramas de atualização; entretanto, os diagramas de atualização já fornecem um modo mais avançado de tratar valores de GUID e identidade.  
  
 As anotações **sql:identity** e **sql:guid** podem ser definidas em um elemento de conteúdo complexo.  
  
## <a name="sqlidentity-annotation"></a>Anotação sql:identity  
 Você pode especificar a anotação **sql:identity** no esquema XSD em qualquer nó que mapeie uma coluna de banco de dados do tipo IDENTIDADE. O valor especificado para esta anotação define como a coluna do tipo identidade é atualizada (usando o valor fornecido no gráfico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de atualização para modificar a coluna ou ignorando o valor, nesse caso um valor gerado é usado para esta coluna).  
  
 A anotação **sql:identity** pode ser atribuída a dois valores:  
  
 ignore  
 Direciona o diagrama de atualização para ignorar qualquer valor que seja fornecido no diagrama de atualização para essa coluna e para depender do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar o valor da identidade.  
  
 useValue  
 Direciona o diagrama de atualização para usar o valor que é fornecido no diagrama de atualização para atualizar a coluna do tipo IDENTITY. Um diagrama de atualização não verifica se a coluna é um valor de identidade ou não.  
  
 Se o gráfico de atualização especificar um valor para a coluna tipo identidade, o **sql:identity="useValue"** deve ser especificado no esquema.  
  
## <a name="sqlguid-annotation"></a>Anotação sql:guid  
 Um diagrama de atualização pode fazer o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerar um valor de GUID e então usar esse valor no diagrama de atualização. No contexto do DiffGrams, você pode usar a anotação **sql:guid** para especificar se deve usar um valor GUID gerado pelo SQL Server ou usar o valor fornecido no updategram para essa coluna.  
  
 A anotação **sql:guid** pode ser atribuída a dois valores:  
  
 generate  
 Especifica que o GUID gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja usado para essa coluna na operação de atualização.  
  
 useValue  
 Especifica que o valor especificado no diagrama de atualização seja usado para a coluna. Esse é o valor padrão.  
  
  
