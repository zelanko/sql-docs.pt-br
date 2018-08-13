---
title: Excluindo dados usando diagramas de atualização XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 462aae19c9c01ef4b4eb3cd4ccc01ddd6a3e07d3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559136"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Excluindo dados usando diagramas de atualização XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um diagrama de atualização indica uma operação de exclusão quando uma instância de registro aparece na  **\<antes de >** bloco sem registros correspondentes no  **\<depois >** bloco. Nesse caso, o diagrama de atualização exclui o registro na  **\<antes de >** bloco do banco de dados.  
  
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
  
 Você pode omitir as  **\<depois >** marcar se o diagrama estiver executando apenas uma operação de exclusão. Se você não especificar opcional **esquema de mapeamento** atributo, o  **\<ElementName >** especificado no diagrama de atualização mapeará para uma tabela de banco de dados e o mapa de elementos ou atributos filho para colunas da tabela.  
  
 Se um elemento especificado no diagrama corresponde a mais de uma linha na tabela ou não corresponde a nenhuma linha, o diagrama de atualização retornará um erro e cancelará todo o  **\<sincronização >** bloco. Só um registro de cada vez pode ser excluído por um elemento no diagrama.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos desta seção usam o mapeamento padrão (ou seja, nenhum esquema de mapeamento é especificado no diagrama de atualização). Para obter mais exemplos de diagramas de atualização que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Para criar exemplos de funcionamento usando os exemplos a seguir, você deve atender aos requisitos especificados em [requisitos para executar exemplos do SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. Excluindo um registro usando um diagrama de atualização  
 Os diagramas a seguir excluem dois registros da tabela HumanResources.Shift.  
  
 Nestes exemplos, o diagrama não especifica um esquema de mapeamento. Portanto, o diagrama usa o mapeamento padrão no qual o nome de elemento é mapeado para o nome de tabela e os atributos ou subelementos para as colunas.  
  
 Este primeiro diagrama é centrado em atributo e identifica dois turnos (dia-tarde e tarde-noite) na  **\<antes de >** bloco. Porque não há nenhum registro correspondente a  **\<depois >** bloco, essa é uma operação de exclusão.  
  
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
  
1.  Conclua o exemplo B ("Inserindo vários registros usando um diagrama de atualização") no [inserindo dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copie o updategram acima no bloco de notas e salve-o como Updategram-Removeshifts na mesma pasta que foi usada para concluir ("Inserindo vários registros usando um diagrama de atualização") no [inserindo dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
