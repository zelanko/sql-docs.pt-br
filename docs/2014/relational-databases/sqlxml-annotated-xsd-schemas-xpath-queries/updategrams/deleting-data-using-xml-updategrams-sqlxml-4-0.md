---
title: Excluindo dados usando Updategrams XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f83676f981742158ffad7f2d9ac5b50949172fd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060074"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Excluindo dados usando diagramas de atualização XML (SQLXML 4.0)
  Um updategram indica uma operação de exclusão quando uma instância de registro é exibida no **\<before>** bloco sem registros correspondentes no **\<after>** bloco. Nesse caso, o updategram exclui o registro no **\<before>** bloco do banco de dados.  
  
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
  
 Você pode omitir a **\<after>** marca se o updategram estiver executando apenas uma operação de exclusão. Se você não especificar o atributo opcional `mapping-schema` , o **\<ElementName>** especificado no updategram será mapeado para uma tabela de banco de dados e os elementos filho ou atributos são mapeados para colunas na tabela.  
  
 Se um elemento especificado no updategram corresponder a mais de uma linha na tabela ou não corresponder a nenhuma linha, o updategram retornará um erro e cancelará o **\<sync>** bloco inteiro. Só um registro de cada vez pode ser excluído por um elemento no diagrama.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos desta seção usam o mapeamento padrão (ou seja, nenhum esquema de mapeamento é especificado no diagrama de atualização). Para obter mais exemplos de Updategrams que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um Updategram &#40;SQLXML 4,0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Para criar exemplos de trabalho usando os exemplos a seguir, você deve atender aos requisitos especificados em [requisitos para executar exemplos do SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>a. Excluindo um registro usando um diagrama de atualização  
 Os diagramas a seguir excluem dois registros da tabela HumanResources.Shift.  
  
 Nestes exemplos, o diagrama não especifica um esquema de mapeamento. Portanto, o diagrama usa o mapeamento padrão no qual o nome de elemento é mapeado para o nome de tabela e os atributos ou subelementos para as colunas.  
  
 Esse primeiro updategram é centrado em atributo e identifica dois turnos (dia-noite e noite-noturna) no **\<before>** bloco. Como não há nenhum registro correspondente no **\<after>** bloco, essa é uma operação de exclusão.  
  
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
  
1.  Conclua o exemplo B ("inserindo vários registros usando um updategram") em [inserindo dados usando os UPDATEGRAMS XML &#40;SQLXML 4,0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copie o updategram acima para o bloco de notas e salve-o como Updategram-RemoveShifts.xml na mesma pasta que foi usada para concluir ("inserindo vários registros usando um updategram") na [inserção de dados usando os UPDATEGRAMS XML &#40;SQLXML 4,0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
