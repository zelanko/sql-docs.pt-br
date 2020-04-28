---
title: Excluindo dados usando Updategrams XML (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ad537d8b2ce247d45e8e7a94216006023373c13c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75252427"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Excluindo dados usando diagramas de atualização XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um updategram indica uma operação de exclusão quando uma instância de registro é exibida no bloco ** \<before>** sem registros correspondentes no bloco ** \<After>** . Nesse caso, o updategram exclui o registro no bloco ** \<before>** do banco de dados.  
  
 Este é o formato do diagrama de atualização em uma operação de exclusão:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 Você pode omitir a marca de ** \<>após** se o updategram estiver executando apenas uma operação de exclusão. Se você não especificar o atributo de **esquema de mapeamento** opcional, o ** \<ElementName>** especificado no updategram será mapeado para uma tabela de banco de dados e os elementos filho ou atributos são mapeados para colunas na tabela.  
  
 Se um elemento especificado no updategram corresponder a mais de uma linha na tabela ou não corresponder a nenhuma linha, o updategram retornará um erro e cancelará todo ** \<** o bloco de>de sincronização. Só um registro de cada vez pode ser excluído por um elemento no diagrama.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos desta seção usam o mapeamento padrão (ou seja, nenhum esquema de mapeamento é especificado no diagrama de atualização). Para obter mais exemplos de Updategrams que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Para criar exemplos de trabalho usando os exemplos a seguir, você deve atender aos requisitos especificados em [requisitos para executar exemplos do SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. Excluindo um registro usando um diagrama de atualização  
 Os diagramas a seguir excluem dois registros da tabela HumanResources.Shift.  
  
 Nestes exemplos, o diagrama não especifica um esquema de mapeamento. Portanto, o diagrama usa o mapeamento padrão no qual o nome de elemento é mapeado para o nome de tabela e os atributos ou subelementos para as colunas.  
  
 Esse primeiro updategram é centrado em atributo e identifica dois turnos (dia-noite e noite-noturna) no bloco ** \<antes de>** . Como não há registro correspondente no bloco ** \<After>** , essa é uma operação de exclusão.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Conclua o exemplo B ("inserindo vários registros usando um updategram") em [inserindo dados usando os UPDATEGRAMS XML &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copie o updategram acima para o bloco de notas e salve-o como Updategram-RemoveShifts. xml na mesma pasta usada para concluir ("inserindo vários registros usando um updategram") em [inserindo dados usando os UPDATEGRAMS xml &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
