---
title: Assistente de exportação e importação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f3ce90e2670357d0842b0a6ac7838f396465bab
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380953"
---
# <a name="sql-server-import-and-export-wizard"></a>Assistente de Importação e Exportação do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard oferece o método mais simples para criar um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacote que copia dados de uma origem para um destino.  
  
> [!NOTE]  
>  Em um computador de 64 bits, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala a versão de 64 bits do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DTSWizard.exe). No entanto, algumas fontes de dados, como Access ou Excel, só têm um provedor de 32 bits disponível. Para funcionar com essas fontes de dados, talvez seja necessário instalar e executar a versão de 32 bits do assistente. Para instalar a versão de 32 bits do assistente, selecione Ferramentas de Cliente ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante a instalação.  
  
 Você pode iniciar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no menu Iniciar, do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou no prompt de comando. Para obter mais informações, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode copiar dados de e em qualquer fonte de dados para a qual um provedor de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] gerenciado ou um provedor OLE DB nativo está disponível. A lista de provedores disponíveis inclui as seguintes fontes de dados:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Arquivos simples  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 Alguns recursos de assistente funcionam de forma diferente, dependendo do ambiente em que o assistente é iniciado:  
  
-   Se você iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de importação e exportação no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você executa o pacote imediatamente, selecionando a **executados imediatamente** caixa de seleção. Por padrão, essa caixa de seleção é marcada e o pacote é executado imediatamente.  
  
     Você também pode decidir se deseja salvar o pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou ao sistema de arquivos. Se você optar por salvar o pacote, também deverá especificar um nível de proteção de pacote. Para obter mais informações sobre níveis de proteção do pacote, consulte [controle de acesso para dados confidenciais em pacotes](../security/access-control-for-sensitive-data-in-packages.md).  
  
     Depois que o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver criado o pacote e copiado os dados, você pode usar o [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer para abrir e alterar o pacote salvo com a adição de tarefas, transformações e lógica controlada por evento.  
  
    > [!NOTE]  
    >  No [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a opção para salvar o pacote criado pelo assistente não está disponível.  
  
-   Se você iniciar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o pacote não poderá ser executado como uma etapa na conclusão do assistente. Em vez disso, o pacote será adicionado ao projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir do qual você iniciou o assistente. Você pode então executar o pacote ou estendê-lo adicionando tarefas, transformações e lógica controlada por evento usando o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Para obter mais informações, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>Permissões exigidas pelo Assistente de Importação e Exportação  
 Para concluir o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com sucesso, você deve ter pelo menos as seguintes permissões:  
  
-   Permissões para se conectar aos bancos de dados de origem e destino ou compartilhamentos de arquivos. No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], isso requer direitos de logon de servidor e banco de dados.  
  
-   Permissão para ler dados do banco de dados de origem ou arquivo. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], isso requer permissões SELECT nas tabelas de origem e exibições.  
  
-   Permissões de gravação de dados no banco de dados ou arquivo de destino. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], isto requer permissões INSERT nas tabelas de destino.  
  
-   Se você desejar criar um novo banco de dados, tabela ou arquivo de destino, é necessário ter as permissões suficientes para criar o banco de dados, a tabela ou o arquivo. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], isso requer permissões CREATE DATABASE ou CREATE TABLE.  
  
-   Se você deseja salvar o pacote criado pelo assistente, as permissões suficientes para gravar no banco de dados msdb ou no sistema de arquivos. No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], isso requer permissões INSERT no banco de dados msdb.  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>Mapeando tipos de dados no Assistente de Importação e Exportação  
 O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece poucos recursos de transformação. Com exceção da configuração do nome, do tipo de dados e das propriedades de tipo de dados das colunas em novas tabelas e arquivos de destino, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte a nenhuma transformação de nível de coluna.  
  
 O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa os arquivos de mapeamento fornecidos pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para mapear tipos de dados de uma versão de banco de dados ou sistema para outra. Por exemplo, é possível mapear do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o Oracle. Por padrão, os arquivos de mapeamento no formato XML serão instalados em C:\Arquivos de Programas\Microsoft SQL Server\100\DTS\MappingFiles. Se sua empresa exigir diferentes mapeamentos entre tipos de dados, você poderá atualizá-los para afetar os mapeamentos executados pelo assistente. Por exemplo, se você quiser que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** tipo de dados para mapear para o DB2 **gráficos** tipo de dados, em vez do DB2 **VARGRAPHIC** ao transferir dados do tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para DB2, altere o **nchar** mapeamento no arquivo de mapeamento SqlClientToIBMDB2.xml para usar **gráficos** em vez de **VARGRAPHIC.**  
  
 O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui mapeamentos entre várias combinações de origem e destino usadas geralmente e é possível adicionar novos arquivos de mapeamento ao diretório Mapping Files para oferecer suporte a outras fontes e destinos. Os novos arquivos de mapeamento devem estar em conformidade com o esquema XSD publicado e devem mapear uma combinação exclusiva de origem e destino.  
  
> [!NOTE]  
>  Se você editar um arquivo de mapeamento existente ou adicionar um novo arquivo de mapeamento à pasta, feche e reabra o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para que os arquivos novos ou alterados sejam reconhecidos.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Vídeo, [exportando dados do SQL Server para o Excel (vídeo do SQL Server)](https://go.microsoft.com/fwlink/?LinkID=200975), em technet.microsoft.com  
  
-   Exemplo do CodePlex, [exportando do ODBC para um arquivo simples usando um Tutorial do assistente: Pacotes de lição](https://go.microsoft.com/fwlink/?LinkId=217657), em msftisprodsamples.codeplex.com  
  
  
