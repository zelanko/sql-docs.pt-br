---
title: SQL Server XML Bulk Load objeto modelo (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bf68b7f2c8fd1a2cc8d753ddd6348e8161b55c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013289"
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>Modelo de objeto de carregamento em massa de XML do SQL Server (SQLXML 4.0)
  A Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consiste em modelo de objeto de carregamento em massa de XML do objeto SQLXMLBulkLoad. Esse objeto suporta os métodos e propriedades a seguir.  
  
## <a name="methods"></a>Métodos  
 Execute (executar)  
 Carrega em massa os dados usando o arquivo de esquema e o arquivo de dados (ou fluxo) que são fornecidos como parâmetros.  
  
## <a name="properties"></a>Propriedades  
 BulkLoad  
 Especifica se um Carregamento em Massa deveria ser executado. Essa propriedade é útil se você quiser gerar esquemas (consulte as propriedades SchemaGen, SGDropTables e SGUseID que seguem) e não executar um carregamento em massa. Essa é uma propriedade booliana. Quando a propriedade é definida como TRUE, o Carregamento em Massa de XML é executado. Quando é definida como FALSE, o Carregamento em Massa de XML não é executado.  
  
 O valor padrão é TRUE.  
  
 CheckConstraints  
 Especifica se as restrições (como aquelas devidas ao relacionamento de chave primária/chave estrangeira entre as colunas) definidas na coluna devem ser verificadas quando o Carregamento em Massa de XML insere dados nas colunas. Essa é uma propriedade booliana.  
  
 Quando a propriedade é definida como TRUE, o Carregamento em Massa de XML verifica as restrições para cada valor inserido (o que significa que uma violação de restrição resulta em erro).  
  
> [!NOTE]  
>  Para deixar essa propriedade como FALSE, você deve ter **ALTER TABLE** permissões nas tabelas de destino. Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 O valor padrão é FALSE. Quando ele é definido como FALSE, o Carregamento em Massa de XML ignora as restrições durante uma operação de inserção. Na implementação atual, você precisa definir as tabelas na ordem dos relacionamentos de chave primária e chave estrangeira no esquema de mapeamento. Isso quer dizer que uma tabela com uma chave primária precisa ser definida antes da tabela correspondente com a chave estrangeira, senão haverá falha no Carregamento em Massa de XML.  
  
 Observe que, se a Propagação de ID estiver sendo feita, essa opção não se aplicará e a verificação de restrição será deixada ativada. Isso ocorre quando `KeepIdentity=False` e quando há um relacionamento definido em que o pai é um campo de identidade e o valor é atribuído ao filho enquanto ele é gerado.  
  
 ConnectionCommand  
 Identifica um objeto de conexão existente (por exemplo, o objeto ADO ou ICommand comando) que o XML Bulk Load deve usar. Você pode usar a propriedade ConnectionCommand em vez de especificar uma cadeia de caracteres de conexão com a propriedade ConnectionString. A propriedade de transação deve ser definida como TRUE, se você usar ConnectionCommand.  
  
 Se você usar as propriedades de ConnectionString e ConnectionCommand, o XML Bulk Load usa a última propriedade especificada.  
  
 O valor padrão é NULL.  
  
 ConnectionString  
 Identifica a cadeia de conexão de OLE DB que fornece as informações necessárias para estabelecer uma conexão com uma instância do banco de dados. Se você usar as propriedades de ConnectionString e ConnectionCommand, o XML Bulk Load usa a última propriedade especificada.  
  
 O valor padrão é NULL.  
  
 ErrorLogFile  
 Especifica o nome do arquivo no qual o Carregamento em Massa de XML registra em log os erros e mensagens. O padrão é uma cadeia de caracteres vazia, caso em que não ocorre nenhum registro em log.  
  
 FireTriggers  
 Especifica se os gatilhos definidos nas tabelas de destino deveriam ser acionados durante a operação de Carregamento em Massa. O padrão é FALSE.  
  
 Quando definido como TRUE, os gatilhos serão acionados normalmente durante operações de inserção.  
  
> [!NOTE]  
>  Para deixar essa propriedade como FALSE, você deve ter **ALTER TABLE** permissões nas tabelas de destino. Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 Observe que, se a Propagação de ID estiver sendo feita, essa opção não se aplicará, e os gatilhos serão deixados ativados. Isso ocorre quando `KeepIdentity=False` e quando há um relacionamento definido em que o pai é um campo de identidade e o valor é atribuído ao filho enquanto ele é gerado.  
  
 ForceTableLock  
 Especifica se as tabelas nas quais o Carregamento em Massa de XML copia dados deveriam ser bloqueadas durante essa atividade. Essa é uma propriedade booliana. Quando a propriedade é definida como TRUE, o Carregamento em Massa de XML adquire bloqueios de tabela durante essa atividade. Quando é definido como FALSE, o Carregamento em Massa de XML adquire um bloqueio de tabela sempre que insere um registro em uma tabela.  
  
 O valor padrão é FALSE.  
  
 IgnoreDuplicateKeys  
 Especifica o que fazer se houver uma tentativa de inserir valores duplicados em uma coluna de chave. Se essa propriedade for definida como TRUE e houver uma tentativa de inserir um registro com um valor duplicado em uma coluna de chave, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não inserirá esse registro. Entretanto, ela não insere o registro subsequente, por isso a operação de Carregamento em Massa não apresenta falha. Se essa propriedade for definida como FALSE, o Carregamento em Massa falhará quando houver uma tentativa de inserir um valor duplicado em uma coluna de chave.  
  
 Quando a propriedade IgnoreDuplicateKeys é definida como TRUE, uma instrução COMMIT é emitida para cada registro inserido na tabela. Isso diminui o desempenho. A propriedade pode ser definida como TRUE, somente quando a propriedade de transação é definida como FALSE, pois o comportamento transacional é implementado usando arquivos.  
  
 O valor padrão é FALSE.  
  
 KeepIdentity  
 Especifica como lidar com os valores para uma coluna de tipo de Identidade no arquivo de origem. Essa é uma propriedade booliana. Quando a propriedade é definida como TRUE, o Carregamento em Massa de XML atribui à coluna de identidade os valores especificados no arquivo de origem. Quando a propriedade é definida como FALSE, a operação de carregamento em massa ignora os valores da coluna de identidade especificados na origem. Nesse caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] atribui um valor à coluna de identidade.  
  
 Se o Carregamento em Massa envolver uma coluna que consiste em uma chave estrangeira referindo-se a uma coluna de identidade na qual estão armazenados valores gerados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o Carregamento em Massa propagará adequadamente esses valores de identidade para a coluna de chave estrangeira.  
  
 O valor dessa propriedade se aplica a todas as colunas envolvidas no carregamento em massa. O valor padrão é TRUE.  
  
> [!NOTE]  
>  Para deixar essa propriedade como TRUE, você deve ter **ALTER TABLE** permissões nas tabelas de destino. Caso contrário, será preciso defini-la com um valor de FALSE. Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 KeepNulls  
 Especifica qual valor usar para uma coluna que está perdendo um elemento filho ou atributo correspondente no documento XML. Essa é uma propriedade booliana. Quando a propriedade é definida como TRUE, o Carregamento em Massa de XML atribui um valor nulo à coluna. Ele não atribui o eventual valor padrão da coluna conforme definido no servidor. O valor dessa propriedade se aplica a todas as colunas envolvidas no carregamento em massa.  
  
 O valor padrão é FALSE.  
  
 SchemaGen  
 Especifica se as tabelas necessárias serão criadas antes de executar uma operação de Carregamento em Massa. Essa é uma propriedade booliana. Se essa propriedade for definida como TRUE, serão criadas as tabelas identificadas no esquema de mapeamento (o banco de dados deve existir). Se já existirem um ou mais das tabelas no banco de dados, a propriedade SGDropTables determina se essas tabelas preexistentes devem ser descartadas e recriadas.  
  
 O valor padrão para a propriedade SchemaGen é FALSE. SchemaGen não cria restrições de chave primária nas tabelas recém-criado. SchemaGen, no entanto, criar restrições FOREIGN KEY no banco de dados se conseguir encontrar correspondência `sql:relationship` e `sql:key-fields` anotações no esquema de mapeamento e se o campo de chave consiste em uma única coluna.  
  
 Observe que, se você definir a propriedade SchemaGen como TRUE, o XML Bulk Load faz o seguinte:  
  
-   Cria as tabelas necessárias com os nomes de atributo e elemento. Por isso, é importante que você não use palavras reservadas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para nomes de atributo e elemento no esquema.  
  
-   Retorna dados de estouro para qualquer coluna designada usando o [SQL: overflow-campo](annotation-interpretation-sql-overflow-field.md) na [tipo de dados xml](/sql/t-sql/xml/xml-transact-sql) formato.  
  
 SGDropTables  
 Especifica se as tabelas existentes devem ser descartadas e recriadas. Você usa essa propriedade quando a propriedade SchemaGen é definida como TRUE. Se SGDropTables for FALSE, as tabelas existentes serão retidas. Quando essa propriedade for TRUE, as tabelas existentes serão excluídas e recriadas.  
  
 O valor padrão é FALSE.  
  
 SGUseID  
 Especifica se o atributo no esquema de mapeamento identificado como de tipo `id` pode ser usado na criação de uma restrição de PRIMARY KEY quando a tabela é criada. Use essa propriedade quando a propriedade SchemaGen é definida como TRUE. Se SGUseID for TRUE, o utilitário de SchemaGen usa um atributo para o qual `dt:type="id"` é especificada como coluna de chave primária e adiciona a restrição de chave primária apropriada ao criar a tabela.  
  
 O valor padrão é FALSE.  
  
 TempFilePath  
 Especifica o caminho do arquivo onde o Carregamento em Massa de XML cria os arquivos temporários para um carregamento em massa transacionado. (Essa propriedade é útil somente quando a propriedade de transação é definida como TRUE.) Você deve garantir que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta que é usada para o XML Bulk Load tenha acesso a esse caminho. Se essa propriedade não for definida, o Carregamento em Massa de XML armazenará os arquivos temporários no local especificado na variável de ambiente TEMP.  
  
 Transaction  
 Especifica se o Carregamento em Massa deveria ser executado como uma transação, caso em que a reversão será garantida se houver falha do Carregamento em Massa. Essa é uma propriedade booliana. Se a propriedade for definida como TRUE, o Carregamento em Massa ocorrerá em um contexto transacional. A propriedade TempFilePath é útil somente quando a transação é definida como TRUE.  
  
> [!NOTE]  
>  Se você estiver carregando dados binários (como hex e bin.base64 tipos de dados XML para o binário, imagem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados), a propriedade de transação deve ser definida como FALSE.  
  
 O valor padrão é FALSE.  
  
 XMLFragment  
 Especifica se os dados de origem são um fragmento XML. Um fragmento XML é um documento XML sem nenhum elemento de nível superior (raiz). Essa é uma propriedade booliana. Essa propriedade precisa ser definida como TRUE se o arquivo de origem consistir em um fragmento XML.  
  
 O valor padrão é FALSE.  
  
  
