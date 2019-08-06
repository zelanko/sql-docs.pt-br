---
title: Criar, alterar e remover FileTables | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 494eabcd54e7a8c28b3a68e99efca72ef80eb9e1
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811243"
---
# <a name="create-alter-and-drop-filetables"></a>Criar, alterar e remover FileTables
  Descreve como criar uma nova FileTable, ou alterar ou remover uma FileTable existente.  
  
##  <a name="BasicsCreate"></a> Criando uma FileTable  
 Uma FileTable é uma tabela de usuário especializada que tem um esquema predefinido e fixo. Esse esquema armazena dados FILESTREAM, informações de arquivo e diretório e atributos de arquivo. Para obter informações sobre o esquema do FileTable, consulte [FileTable Schema](filetable-schema.md).  
  
 Você pode criar uma nova FileTable usando Transact-SQL ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Como uma FileTable tem um esquema fixo, você não precisa especificar uma lista de colunas. A sintaxe simples de criação de uma FileTable permite que você especifique:  
  
-   Um nome de diretório. Na hierarquia de pastas de FileTable, esse diretório em nível de tabela se torna o filho do diretório de banco de dados especificado no nível de banco de dados, e o pai dos arquivos ou diretórios armazenados na tabela.  
  
-   O nome da ordenação a ser usado para nomes de arquivo na coluna **Name** da FileTable.  
  
-   Os nomes a serem usados para as 3 chaves primária e restrições exclusivas que são criadas automaticamente.  
  
###  <a name="HowToCreate"></a> Como criar uma FileTable  
 **Criar uma FileTable usando Transact-SQL**  
 Crie uma FileTable chamando a instrução [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) com a opção **AS FileTable**. Como uma FileTable tem um esquema fixo, você não precisa especificar uma lista de colunas. Você pode especificar as seguintes configurações para a nova FileTable:  
  
1.  **FILETABLE_DIRECTORY**. Especifica o diretório que atua como diretório raiz de todos os arquivos e diretórios armazenados na FileTable. Esse nome deve ser exclusivo entre todos os nomes de diretórios de FileTable no banco de dados. A comparação de exclusividade não diferencia maiúsculas de minúsculas, independentemente das configurações de ordenação atuais.  
  
    -   Esse valor tem um tipo de dados **nvarchar(255)** e usa uma ordenação fixa de **Latin1_General_CI_AS_KS_WS**.  
  
    -   O nome de diretório que você fornece deve atender aos requisitos do sistema de arquivos para um nome de diretório válido.  
  
    -   Esse nome deve ser exclusivo entre todos os nomes de diretórios de FileTable no banco de dados. A comparação de exclusividade não diferencia maiúsculas de minúsculas, independentemente das configurações de ordenação atuais.  
  
    -   Se você não fornecer um nome de diretório ao criar a FileTable, o nome da FileTable será usado como nome do diretório.  
  
2.  **FILETABLE_COLLATE_FILENAME**. Especifica o nome da ordenação a ser aplicado à coluna **Name** da FileTable.  
  
    1.  A ordenação especificada não deve fazer **diferenciação de maiúsculas e minúsculas** para estar em conformidade com a semântica de nomenclatura de arquivo do Windows.  
  
    2.  Se você não fornecer um valor para **FILETABLE_COLLATE_FILENAME** ou se você especificar **database_default**, a coluna herdará a ordenação do banco de dados atual. Se a ordenação do banco de dados atual diferenciar maiúsculas de minúsculas, será gerado um erro e a operação **CREATE TABLE** falhará.  
  
3.  Você também pode especificar os nomes a serem usados para as 3 restrições de chave primária e exclusivas que são criadas automaticamente. Se você não fornecer nomes, o sistema gerará nomes conforme descrito posteriormente neste tópico.  
  
    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **Exemplos**  
  
 O exemplo a seguir cria uma nova FileTable e especifica valores definidos pelo usuário para **FILETABLE_DIRECTORY** e **FILETABLE_COLLATE_FILENAME**.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 O exemplo a seguir também cria uma nova FileTable. Como os valores definidos pelo usuário não são especificados, o nome de **FILETABLE_DIRECTORY** se torna o nome do FileTable, o valor de **FILETABLE_COLLATE_FILENAME** se torna database_default e a chave primária e as restrições exclusivas recebem nomes gerados pelo sistema.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **Criar uma FileTable usando o SQL Server Management Studio**  
 No Pesquisador de Objetos, expanda os objetos do banco de dados selecionado, clique com o botão direito do mouse na pasta **Tabelas** e selecione **Nova FileTable**.  
  
 Esta opção abre uma nova janela de script que contém um modelo de script Transact-SQL que você pode personalizar e executar para criar uma FileTable. Use a opção **Especificar Valores para Parâmetros de Modelo** no menu **Consulta** para personalizar facilmente o script.  
  
###  <a name="ReqCreate"></a> Requisitos e restrições para a criação de uma FileTable  
  
-   Você não pode alterar uma tabela existente para convertê-la em uma FileTable.  
  
-   O diretório pai especificado anteriormente no nível do banco de dados deve ter um valor não nulo. Para obter informações sobre a especificação do diretório no nível de banco de dados, consulte [Habilitar os pré-requisitos para FileTable](enable-the-prerequisites-for-filetable.md).  
  
-   Uma FileTable requer um grupo de arquivos FILESTREAM válido, já que uma FileTable contém uma coluna FILESTREAM. Opcionalmente, você pode especificar um grupo de arquivos FILESTREAM válido como parte do comando **CREATE TABLE** para criação de uma FileTable. Se você não especificar um grupo de arquivos, a FileTable usará o grupo de arquivos FILESTREAM padrão para o banco de dados. Se o banco de dados não tiver um grupo de arquivos FILESTREAM, será gerado um erro.  
  
-   Não é possível criar uma restrição de tabela como parte de uma instrução **CREATE TABLE...AS FILETABLE**. No entanto, você pode adicionar a restrição posteriormente usando uma instrução **ALTER TABLE** .  
  
-   Não é possível criar uma FileTable no banco de dados **tempdb** ou em qualquer outro banco de dados do sistema.  
  
-   Você não pode criar uma FileTable como uma tabela temporária.  
  
##  <a name="BasicsAlter"></a> Alterando uma FileTable  
 Como uma FileTable tem um esquema predefinido e fixo, você não pode adicionar nem alterar suas colunas. No entanto, você pode adicionar índices personalizados, gatilhos, restrições e outras opções a uma FileTable.  
  
 Para obter informações sobre como usar a instrução ALTER TABLE para habilitar ou desabilitar o namespace da FileTable, incluindo as restrições definidas pelo sistema, consulte [Gerenciar FileTables](manage-filetables.md).  
  
###  <a name="HowToChange"></a> Como alterar o diretório de uma FileTable  
 **Alterar o diretório para uma FileTable usando Transact-SQL**  
 Chame a instrução ALTER TABLE e forneça um novo valor válido para a opção **FILETABLE_DIRECTORY** SET.  
  
 **Exemplo**  
  
```sql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **Alterar um diretório para uma FileTable usando o SQL Server Management Studio**  
 No Explorador de Objetos, clique com o botão direito do mouse em FileTable e selecione **Propriedades** para abrir a caixa de diálogo **Propriedades de Tabela** . Na página **FileTable** , insira um novo valor para o **Nome de diretório da FileTable**.  
  
###  <a name="ReqAlter"></a> Requisitos e restrições para alterar uma FileTable  
  
-   Você não pode alterar o valor de **FILETABLE_COLLATE_FILENAME**.  
  
-   Você não pode alterar, remover ou desabilitar as colunas definidas pelo sistema de uma FileTable.  
  
-   Você não pode adicionar novas colunas de usuário, colunas computadas ou colunas computadas persistentes a uma FileTable.  
  
##  <a name="BasicsDrop"></a> Removendo uma FileTable  
 Você pode remover uma FileTable usando a sintaxe normal da instrução [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql).  
  
 Quando você remover uma FileTable, os seguintes objetos também serão removidos:  
  
-   Todas as colunas da FileTable e todos os objetos associados à tabela, como índices, restrições e gatilhos, também serão removidos.  
  
-   O diretório da FileTable e seus subdiretórios desaparecerão do arquivo FILESTREAM e da hierarquia de diretórios do banco de dados.  
  
 O comando DROP TABLE falhará se houver identificadores de arquivos abertos no namespace de arquivo da FileTable. Para obter mais informações sobre o fechamento de identificadores abertos, consulte [Gerenciar FileTables](manage-filetables.md).  
  
##  <a name="BasicsOtherObjects"></a> Outros objetos de banco de dados são criados quando você cria uma FileTable  
 Quando você cria uma nova FileTable, também são criados alguns índices e restrições definidos pelo sistema. Você não pode alterar ou remover esses objetos. Eles desaparecem apenas quando a própria FileTable é removida. Para ver a lista desses objetos, consulte a exibição de catálogo [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql).  
  
```sql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **Índices que são criados quando você cria uma nova FileTable**  
 Quando você cria uma nova FileTable, os seguintes índices definidos pelo sistema também são criados:  
  
|||  
|-|-|  
|**Colunas**|**Tipo de índice**|  
|[path_locator] ASC|Chave primária, não clusterizado|  
|[parent_path_locator] ASC,<br /><br /> [name] ASC|Exclusivo, não clusterizado|  
|[stream_id] ASC|Exclusivo, não clusterizado|  
  
 **Restrições que são criadas quando você cria uma nova FileTable**  
 Quando você cria uma nova FileTable, as seguintes restrições definidas pelo sistema também são criadas:  
  
|Restrições|Impõe|  
|-----------------|--------------|  
|Restrições padrão nas seguintes colunas:<br /><br /> **creation_time** <br /> **is_archive** <br /> **is_directory** <br /> **is_hidden** <br /> **is_offline** <br /> **is_readonly** <br /> **is_system** <br /> **is_temporary** <br /> **last_access_time** <br /> **last_write_time** <br /> **path_locator** <br /> **stream_id**|As restrições padrão definidas pelo sistema impõem valores padrão para as colunas especificadas.|  
|Verificar restrições|As restrições de verificação definidas pelo sistema impõem os seguintes requisitos:<br /><br /> Nomes de arquivo válidos.<br /><br /> Atributos de arquivo válidos.<br /><br /> O objeto pai deve ser um diretório.<br /><br /> A hierarquia de namespaces é bloqueada durante a manipulação do arquivo.|  
  
 **Convenção de nomenclatura para as restrições definidas pelo sistema**  
 As restrições definidas pelo sistema descritas acima são nomeadas no formato **\<constraintType>_\<tablename>[\_\<columnname>]\_\<uniquifier>** , em que:  
  
-   *<constraint_type>* é CK (restrição de verificação), DF (restrição padrão), FK (chave estrangeira), PK (chave primária) ou UQ (restrição exclusiva).  
  
-   *\<uniquifier>* é uma cadeia de caracteres gerada pelo sistema para tornar o nome exclusivo. Essa cadeia de caracteres pode conter o nome e um identificador exclusivo da FileTable.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar FileTables](manage-filetables.md)  
  
  
