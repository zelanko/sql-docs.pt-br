---
title: Converter esquemas XDR anotados em XSD (SQLXML)
description: Saiba como converter um esquema XDR anotado em um esquema XSD equivalente usando a ferramenta de conversor XDR para XSD no SQLXML 4,0.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d7936bf8d9d9c37620ef9b692c125ff16f1cea85
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467107"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>Convertendo esquemas XDR anotados a esquemas XSD equivalentes (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  A linguagem XSD é a sucessora da linguagem XDR. Com a introdução do suporte a XSD no SQLXML 4.0 do [!INCLUDE[msCoName](../../../includes/msconame-md.md)], supõe-se a criação de novos esquemas anotados usando XSD. O SQLXML 4.0 inclui uma ferramenta de conversão de XDR para XSD projetada para ajudá-lo a converter os esquemas XDR anotados em esquemas XSD equivalentes.  
  
> [!IMPORTANT]  
>  Só use essa ferramenta quando quiser converter esquemas XDR anotados em XSD a serem usados o com SQLXML 4.0. Não se trata de uma ferramenta de conversão de XDR em XSD de uso geral. Os esquemas XSD convertidos talvez não se comportem da mesma forma que os esquemas XDR originais quando usados em outros ambientes.  
  
 Caso o arquivo XDR de entrada especifique a codificação na declaração XML, esta se torna a codificação do arquivo de saída XSD gerado.  
  
 A ferramenta de conversão (Cvtschema.exe) é instalada na pasta Arquivos de Programa\SQLXML 4.0\bin, sendo executada no prompt de comando.  
  
 Esta é a sintaxe geral:  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 Em que:  
  
 XDRFileName  
 É o nome do arquivo XDR a ser convertido em XSD. A ferramenta lê o arquivo XDR de entrada e cria um arquivo de saída XSD no diretório funcional atual. Caso o arquivo de entrada tenha uma extensão .xdr ou .xml, o arquivo XSD de saída é criado com o mesmo nome, mas com uma extensão .xsd. Se a extensão de nome de arquivo de entrada for diferente de. xml ou. XDR (ou se a extensão estiver ausente), o arquivo de saída será criado com o mesmo nome e a extensão. xsd será anexada ao nome do arquivo de entrada. Por exemplo, caso o nome de arquivo XDR de entrada seja SampleFile.abc, o XSD resultante é salvo como SampleFile.abc.xsd.  
  
 -y  
 (Opcional) Substitui o arquivo XSD existente pelo arquivo XSD gerado pela ferramenta de conversão. Caso o sinalizador não seja especificado, a ferramenta pede para que você opte por substituir o arquivo existente XSD e lhe dá a opção de alterar o nome do arquivo de saída.  
  
 -w  
 (Opcional) Retorna advertências não fatais geradas no processo de conversão pela ferramenta. Por padrão, a ferramenta só exibe mensagens de erros fatais.  
  
 -?  
 Retorna uma lista de opções que você pode especificar com **cvtschema**, juntamente com uma explicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tipos de dados XSD para tipos de dados XPath &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)   
 [Anotações XSD &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
