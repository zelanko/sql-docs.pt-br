---
title: FileTables (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2016
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3045c125db70625a6c706f14a53cb30333633f24
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423497"
---
# <a name="filetables-sql-server"></a>FileTables (SQL Server)
  O recurso FileTable oferece suporte para namespace de arquivo do Windows e compatibilidade de aplicativos do Windows com dados de arquivo armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O FileTable permite que um aplicativo integre seus componentes de armazenamento e gerenciamento de dados e forneça serviços integrados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , inclusive pesquisa de texto completo e pesquisa semântica, em dados não estruturados e metadados.  
  
 Em outras palavras, você pode armazenar arquivos e documentos em tabelas especiais no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , denominadas FileTables, mas acessá-los a partir de aplicativos do Windows como se eles estivessem armazenados no sistema de arquivos, sem fazer alterações nos seus aplicativos cliente.  
  
 O recurso FileTable se baseia na tecnologia FILESTREAM do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais sobre o FILESTREAM, veja [FILESTREAM &#40;SQL Server&#41;](filestream-sql-server.md).  
  
##  <a name="Goals"></a> Benefícios do recurso FileTable  
 Os objetivos do recurso FileTable incluem o seguinte:  
  
-   Compatibilidade com APIs do Windows para dados de arquivos armazenados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A compatibilidade com APIs do Windows inclui o seguinte:  
  
    -   Acesso de streaming não transacional e atualizações in loco para dados FILESTREAM.  
  
    -   Um namespace hierárquico de diretórios e arquivos.  
  
    -   Armazenamento de atributos de arquivo, como data de criação e data de modificação.  
  
    -   Suporte para APIs de gerenciamento de arquivos e diretórios do Windows.  
  
-   Compatibilidade com outros recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que incluem ferramentas de gerenciamento, serviços e recursos de consulta relacional em dados de atributo de arquivo e FILESTREAM.  
  
 Com isso, as FileTables removem uma barreira significativa ao uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o armazenamento e gerenciamento de dados não estruturados que residem atualmente como arquivos em servidores de arquivos. As empresas podem mover esses dados de servidores de arquivos para FileTables para aproveitar a administração integrada e os serviços fornecidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao mesmo tempo, podem manter a compatibilidade de aplicativos do Windows para seus aplicativos do Windows existentes que consultam esses dados como arquivos no sistema de arquivos.  
    
##  <a name="Description"></a> O que é uma FileTable?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece uma **tabela de arquivos**especial, também chamada de **FileTable**, para aplicativos que exigem o armazenamento de arquivos e diretório no banco de dados, com a compatibilidade de API do Windows e o acesso não transacional. Uma FileTable é uma tabela de usuário especializada com um esquema predefinido que armazena dados FILESTREAM, além de informações de hierarquias de arquivos e diretórios e atributos de arquivos.  
  
 Uma FileTable fornece a seguinte funcionalidade:  
  
-   Uma FileTable representa uma hierarquia de diretórios e arquivos. Armazena dados relacionados a todos os nós dessa hierarquia, tanto aos diretórios quanto aos arquivos que contêm. Essa hierarquia começa em um diretório raiz que você especifica ao criar a FileTable.  
  
-   Cada linha de uma FileTable representa um arquivo ou um diretório.  
  
-   Cada linha contém os seguintes itens: Para obter mais informações sobre o esquema de uma FileTable, veja [Esquema de FileTable](filetable-schema.md).  
  
    -   Uma coluna**file_stream** para dados de fluxo e um identificador (GUID) **stream_id** . (A coluna **file_stream** é NULL para um diretório.)  
  
    -   As colunas **path_locator** e **parent_path_locator** para representar e manter a hierarquia de arquivos e diretórios.  
  
    -   10 atributos de arquivo, como a data de criação e a data de modificação que são úteis com APIs de E/S de arquivo.  
  
    -   Uma coluna de tipo que oferece suporte à pesquisa de texto completo e à pesquisa semântica em arquivos e documentos.  
  
-   Uma FileTable impõe determinados gatilhos e restrições definidos pelo sistema para manter a semântica de namespace de arquivo.  
  
-   Quando o banco de dados é configurado para acesso não transacional, a hierarquia de arquivos e diretórios representada no FileTable é exposta no compartilhamento FILESTREAM configurado para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso oferece ao sistema de arquivos acesso para aplicativos Windows.  
  
 Algumas características adicionais de FileTables incluem o seguinte:  
  
-   Os dados de arquivos e diretórios armazenados em uma FileTable são expostos através de um compartilhamento do Windows para acesso não transacional a arquivos para aplicativos baseados em APIs do Windows. Para um aplicativo do Windows, isto parece um compartilhamento normal com seus arquivos e diretórios. Aplicativos podem usar um conjunto sofisticado de APIs do Windows para gerenciar os arquivos e diretórios neste compartilhamento.  
  
-   A hierarquia de diretórios exposta por meio do compartilhamento é uma estrutura de diretórios puramente lógica que é mantida dentro da FileTable.  
  
-   As chamadas para criar ou alterar um arquivo ou um diretório por meio do compartilhamento Windows são interceptadas por um componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e refletidas nos dados relacionais correspondentes na FileTable.  
  
-   As operações de APIs do Windows são não transacionais por natureza, e não estão associadas a transações de usuário. Entretanto, o acesso transacional a dados FILESTREAM armazenados em uma FileTable tem suporte total, como é o caso para qualquer coluna FILESTREAM em uma tabela normal.  
  
-   FileTables também podem ser consultadas e atualizadas através do acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] normal. Elas também são integradas a ferramentas de gerenciamento e recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como o backup.  
  
  
##  <a name="additional"></a> Considerações adicionais para usar FileTables  
  
###  <a name="DBA"></a> Considerações administrativas  
 **Sobre FILESTREAM e FileTables**  
  
-   Você configura FileTables separadamente de FILESTREAM. Portanto, você pode continuar a usar o recurso FILESTREAM sem habilitar o acesso não transacional ou criar FileTables.  
  
-   Não existe acesso não transacional a dados FILESTREAM, exceto por meio de FileTables. Portanto, quando você habilita o acesso não transacional, o comportamento de colunas FILESTREAM e aplicativos existentes não é afetado.  
  
 **Sobre FileTables e acesso não transacional**  
  
-   É possível habilitar ou desabilitar o acesso não transacional no nível de banco de dados.  
  
-   Você pode configurar ou ajustar o acesso não transacional no nível de banco de dados desativando-o, ou habilitando o acesso somente leitura ou leitura/gravação completa.  
  
  
###  <a name="memory"></a> FileTables não dão suporte a arquivos mapeados por memória  
 FileTables não dão suporte a arquivos mapeados por memória. Bloco de Notas e Paint são dois exemplos comuns de aplicativos que usam arquivos mapeados por memória. Você não pode usar estes aplicativos no mesmo computador que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para abrir arquivos que estão armazenados em um FileTable. Porém, você pode usar estes aplicativos de um computador remoto para abrir arquivos que estão armazenados em um FileTable, porque, nestes circunstâncias, o recurso do mapeamento de memória não é usado.  
  
  
##  <a name="reltasks"></a> Tarefas relacionadas  
 [Habilitar os pré-requisitos para o FileTable](enable-the-prerequisites-for-filetable.md)  
 Descreve como habilitar os pré-requisitos para criar e usar FileTables.  
  
 [Criar, alterar e remover FileTables](create-alter-and-drop-filetables.md)  
 Descreve como criar uma nova FileTable, ou alterar ou remover uma FileTable existente.  
  
 [Carregar arquivos em FileTables](load-files-into-filetables.md)  
 Descreve como carregar ou migrar arquivos para FileTables.  
  
 [Trabalhar com diretórios e caminhos em FileTables](work-with-directories-and-paths-in-filetables.md)  
 Descreve a estrutura de diretórios na qual os arquivos são armazenados em FileTables.  
  
 [Acessar FileTables com Transact-SQL](access-filetables-with-transact-sql.md)  
 Descreve como os comandos DML (linguagem de manipulação de dados) Transact-SQL funcionam com FileTables.  
  
 [Acessar FileTables com APIs de entrada e saída de arquivo](access-filetables-with-file-input-output-apis.md)  
 Descreve como a E/S do sistema de arquivos funciona em uma FileTable.  
  
 [Gerenciar FileTables](manage-filetables.md)  
 Descreve tarefas administrativas comuns para gerenciar FileTables.  
  
  
##  <a name="relcontent"></a> Conteúdo relacionado  
 [Esquema de FileTable](filetable-schema.md)  
 Descreve o esquema predefinido e fixo de uma FileTable.  
  
 [Compatibilidade do FileTable com outros recursos do SQL Server](filetable-compatibility-with-other-sql-server-features.md)  
 Descreve como as FileTables funcionam com outros recursos do SQL Server.  
  
 [DDL, funções, procedimentos armazenados e exibições de FileTable](../views/views.md)  
 Lista as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e os objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram adicionados ou alterados para oferecer suporte ao recurso FileTable.  
  
 
  
