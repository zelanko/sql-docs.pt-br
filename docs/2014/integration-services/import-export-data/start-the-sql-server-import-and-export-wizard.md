---
title: Executar o assistente de importação e exportação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 824642cf50923aa7ec879bfedbbb8f4ceaa6d9f3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62768018"
---
# <a name="run-the-sql-server-import-and-export-wizard"></a>Executar o Assistente de Importação e Exportação do SQL Server
  O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o método mais simples para criar pacotes básicos e copiar dados entre fontes de dados. Para obter mais informações sobre o assistente, consulte [SQL Server assistente de importação e exportação](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)do.  
  
 Para um vídeo que demonstra como usar o SQL Server assistente de importação e exportação do para criar um pacote que exporta dados de um banco de SQL Server para uma planilha do Microsoft Excel, consulte [exportando dados SQL Server para o Excel (SQL Server vídeo)](https://go.microsoft.com/fwlink/?LinkId=131024).  
  
### <a name="to-start-the-sql-server-import-and-export-wizard"></a>Para iniciar o Assistente de Importação e Exportação do SQL Server  
  
-   No menu **Iniciar** , aponte para **todos os programas**, aponte para**Microsoft SQL Server** e clique em **importar e exportar dados**.  
  
     -ou-  
  
     No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse na pasta **pacotes SSIS** e clique em **SSISImport e exportar assistente**.  
  
     -ou-  
  
     No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no menu **projeto** , clique em **SSISImport e exportar assistente**.  
  
     -ou-  
  
     No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao tipo de servidor, expanda bancos de dados, clique com o botão direito do mouse em um banco de dados, aponte para **tarefas**e, em seguida, clique em **Import data** ou **Export data**.  
  
     -ou-  
  
     Em uma janela de prompt de comando, execute o DTSWizard.exe, localizado em C:\Arquivos de Programas\Microsoft SQL Server\100\DTS\Binn.  
  
    > [!NOTE]  
    >  Em um computador de 64 bits, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala a versão de 64 bits do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DTSWizard.exe). No entanto, algumas fontes de dados, como Access ou Excel, só têm um provedor de 32 bits disponível. Para funcionar com essas fontes de dados, talvez seja necessário instalar e executar a versão de 32 bits do assistente. Para instalar a versão de 32 bits do assistente, selecione Ferramentas de Cliente ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante a instalação.  
  
### <a name="to-import-or-export-data-by-using-the-sql-server-import-and-export-wizard"></a>Para importar ou exportar dados usando o Assistente de Importação e Exportação do SQL Server  
  
1.  Inicie o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Nas páginas de assistente correspondentes, selecione uma fonte de dados e um destino de dados.  
  
     As fontes de dados disponíveis incluem provedores de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], provedores OLE DB, provedores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], provedores [!INCLUDE[vstecado](../../includes/vstecado-md.md)], Microsoft Office Excel, Microsoft Office Access e a fonte de arquivos simples. Dependendo da fonte, você define opções como modo de autenticação, nome do servidor, nome do banco de dados e formato do arquivo.  
  
    > [!NOTE]  
    >  O provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Oracle não suporta os tipos de dados Oracle BLOB, CLOB, NCLOB, BFILE e UROWID. Portanto, a origem de OLE DB não pode extrair dados de tabelas que contêm colunas com esses tipos de dados.  
  
     Os destinos de dados disponíveis incluem provedores de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], provedores OLE DB, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, Excel, Access e o destino de arquivos simples.  
  
3.  Defina as opções do tipo de destino que você selecionou.  
  
     Se o destino for um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá especificar os seguintes itens:  
  
    -   Indique se deseja criar um banco de dados novo e definir as propriedades do banco de dados. As propriedades a seguir não podem ser configuradas e o assistente usa os valores padrão especificados:  
  
        |Propriedade|Valor|  
        |--------------|-----------|  
        |Ordenação|Latin1_General_CS_AS_KS_WS|  
        |modelo de recuperação|Completo|  
        |Usar indexação de texto completo|True|  
  
    -   Escolha se deseja copiar dados de tabelas ou exibições ou copiar resultados de consulta.  
  
         Se desejar consultar os dados de origem e copiar os resultados, você poderá criar uma consulta Transact-SQL. Você pode digitar a consulta Transact-SQL manualmente ou usar uma consulta salva em um arquivo. O assistente inclui um recurso de navegação para localizar o arquivo e o assistente abre o arquivo automaticamente e cola seu conteúdo na página do assistente quando você seleciona o arquivo.  
  
         Se a fonte for um provedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)], você também poderá usar a opção para copiar resultados da consulta, fornecendo a cadeia DBCommand como a consulta.  
  
         Se os dados da fonte forem uma exibição, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converterá a exibição automaticamente para uma tabela no destino.  
  
    -   Indique se a tabela de destino será descartada e recriada e se as inserções de identidade serão habilitadas.  
  
    -   Indique se você deseja excluir ou adicionar linhas a uma tabela de destino existente. Se a tabela não existir, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a criará automaticamente.  
  
     Se o destino for um destino de arquivo simples, você poderá especificar os seguintes itens:  
  
    -   Especifique o delimitador de linhas no arquivo de destino.  
  
    -   Especifique o delimitador de colunas no arquivo de destino.  
  
4.  (Opcional) Selecione uma tabela e altere os mapeamentos entre as colunas de origem e destino ou altere os metadados das colunas de destino:  
  
    -   Mapeie as colunas de origem para colunas de destino diferentes.  
  
    -   Altere o tipo de dados na coluna de destino.  
  
    -   Defina o comprimento das colunas com tipos de dados de caractere.  
  
    -   Defina a precisão e a escala das colunas com tipos de dados numéricos.  
  
    -   Especifique se a coluna pode conter valores nulos.  
  
5.  (Opcional) Selecione várias tabelas e atualize os metadados e as opções que serão aplicados a essas tabelas:  
  
    -   Selecione um esquema de destino existente ou forneça um novo esquema ao qual as tabelas serão atribuídas.  
  
    -   Especifique se deseja habilitar as inserções de identidade em tabelas de destino.  
  
    -   Especifique se deseja descartar e recriar tabelas de destino.  
  
    -   Especifique se deseja truncar as tabelas de destino existentes.  
  
6.  Salvar e executar um pacote.  
  
     Se o assistente for iniciado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no prompt de comando, o pacote poderá ser executado imediatamente. Opcionalmente, você pode salvar o pacote no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados **msdb** ou no sistema de arquivos. Para obter mais informações sobre o banco de dados **msdb** , consulte [Gerenciamento de pacotes &#40;&#41;do serviço SSIS ](../service/package-management-ssis-service.md).  
  
     Ao salvar o pacote, você poder definir o nível de proteção do pacote e, se esse nível de proteção usar uma senha, fornecer a senha. Para obter mais informações sobre os níveis de proteção do pacote, consulte [controle de acesso para dados confidenciais em pacotes](../security/access-control-for-sensitive-data-in-packages.md).  
  
     Se o assistente for iniciado a partir de um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], não será possível executar o pacote a partir do assistente. Em vez disso, o pacote será adicionado ao projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir do qual você iniciou o assistente. Você poderá então executar o pacote no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
    > [!NOTE]  
    >  No [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a opção para salvar o pacote criado pelo assistente não está disponível.  
  
## <a name="see-also"></a>Consulte Também  
 [Assistente de importação e exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [Copiar pacotes nas Ferramentas de Dados do SQL Server](../create-packages-in-sql-server-data-tools.md)  
  
  
