---
title: Serialização de XML de objetos de banco de dados CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ad6b9ebaba9f05b0a927cd65f788cdbdb672a6d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130822"
---
# <a name="xml-serialization-from-clr-database-objects"></a>Serialização XML de objetos de banco de dados CLR
  A serialização XML é necessária em dois cenários:  
  
-   Invocação de serviços da Web de objetos CLR (Common Language Runtime).  
  
-   Conversão de um UDT (tipo definido pelo usuário) em XML.  
  
 A execução de serialização XML invocando a classe `XmlSerializer` normalmente gera um assembly de serialização adicional que é sobrecarregado no projeto com o assembly de origem. Entretanto, por questões de segurança, essa sobrecarga é desabilitada no CLR. Portanto, para chamar um serviço web ou executar a conversão de UDT em XML no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o assembly deve ser criado manualmente usando uma ferramenta chamada **Sgen.exe** fornecido com o .NET Framework que gera o necessário assemblies de serialização. Ao invocar `XmlSerializer`, o assembly de serialização precisa ser criado manualmente seguindo estas etapas:  
  
1.  Execute o **Sgen.exe** ferramenta que é fornecida com o .NET Framework SDK para criar o assembly que contém os serializadores XML para o assembly de origem.  
  
2.  Registre o assembly gerado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução `CREATE ASSEMBLY`.  
  
 Para obter informações sobre erros que você pode receber ao executar a serialização de XML, consulte o seguinte artigo do Microsoft Support: ["Não é possível carregar o assembly de serialização gerado dinamicamente"](http://support.microsoft.com/kb/913668).  
  
 Para obter informações sobre tipos de dados não suportados pelo XMLSerializer, consulte o suporte a associação de esquemas XML na documentação do .NET Framework.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a dados de objetos de banco de dados CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
