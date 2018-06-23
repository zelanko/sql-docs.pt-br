---
title: Executar o SQL Server de importação e exportação Assistente | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 817172e78c7f7702aa4dc9d7555b25f6866a6897
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121968"
---
# <a name="run-the-sql-server-import-and-export-wizard"></a>Executar o Assistente de Importação e Exportação do SQL Server
  O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o método mais simples para criar pacotes básicos e copiar dados entre fontes de dados. Para obter mais informações sobre o assistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md).  
  
 Para obter um vídeo que demonstra como usar o Assistente para exportação e importação do SQL Server para criar um pacote que exporte dados de um banco de dados do SQL Server para uma planilha do Microsoft Excel, consulte [exportando dados do SQL Server para o Excel (vídeo do SQL Server)](http://go.microsoft.com/fwlink/?LinkId=131024).  
  
### <a name="to-start-the-sql-server-import-and-export-wizard"></a>Para iniciar o Assistente de Importação e Exportação do SQL Server  
  
-   Sobre o **iniciar** , aponte para **todos os programas**, aponte para**Microsoft SQL Server** e, em seguida, clique em **importar e exportar dados**.  
  
     — ou —  
  
     Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], com o botão direito do **pacotes SSIS** pasta e depois clique em **SSISImport e o Assistente para exportação de**.  
  
     — ou —  
  
     Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no **projeto** menu, clique em **SSISImport e o Assistente para exportação de**.  
  
     — ou —  
  
     Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tipo de servidor, expanda bancos de dados, clique em um banco de dados, aponte para **tarefas**e, em seguida, clique em **importar dados** ou **exportar dados**.  
  
     — ou —  
  
     Em uma janela de prompt de comando, execute o DTSWizard.exe, localizado em C:\Arquivos de Programas\Microsoft SQL Server\100\DTS\Binn.  
  
    > [!NOTE]  
    >  Em um computador de 64 bits, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala a versão de 64 bits do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DTSWizard.exe). No entanto, algumas fontes de dados, como Access ou Excel, só têm um provedor de 32 bits disponível. Para funcionar com essas fontes de dados, talvez seja necessário instalar e executar a versão de 32 bits do assistente. Para instalar a versão de 32 bits do assistente, selecione Ferramentas de cliente ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante a instalação.  
  
### <a name="to-import-or-export-data-by-using-the-sql-server-import-and-export-wizard"></a>Para importar ou exportar dados usando o Assistente de Importação e Exportação do SQL Server  
  
1.  Inicie o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Nas páginas de assistente correspondentes, selecione uma fonte de dados e um destino de dados.  
  
     As fontes de dados disponíveis incluem provedores de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], provedores OLE DB, provedores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], provedores [!INCLUDE[vstecado](../../includes/vstecado-md.md)], Microsoft Office Excel, Microsoft Office Access e a fonte de arquivos simples. Dependendo da fonte, você define opções como modo de autenticação, nome do servidor, nome do banco de dados e formato do arquivo.  
  
    > [!NOTE]  
    >  O provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Oracle não suporta os tipos de dados Oracle BLOB, CLOB, NCLOB, BFILE e UROWID. Portanto, a origem de OLE DB não pode extrair dados de tabelas que contêm colunas com esses tipos de dados.  
  
     Os destinos de dados disponíveis incluem [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] provedores de dados, os provedores OLE DB, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, Excel, Access e o destino de arquivo simples.  
  
3.  Defina as opções do tipo de destino que você selecionou.  
  
     Se o destino for um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá especificar os seguintes itens:  
  
    -   Indique se deseja criar um banco de dados novo e definir as propriedades do banco de dados. As propriedades a seguir não podem ser configuradas e o assistente usa os valores padrão especificados:  
  
        |Propriedade|Valor|  
        |--------------|-----------|  
        |Agrupamento|Latin1_General_CS_AS_KS_WS|  
        |modelo de recuperação|Completo|  
        |Usar indexação de texto completo|True|  
  
    -   Escolha se deseja copiar dados de tabelas ou exibições ou copiar resultados de consulta.  
  
         Se desejar consultar os dados de origem e copiar os resultados, você poderá criar uma consulta Transact-SQL. Você pode digitar a consulta Transact-SQL manualmente ou usar uma consulta salva em um arquivo. O assistente inclui um recurso de navegação para localizar o arquivo e o assistente abre o arquivo automaticamente e cola seu conteúdo na página do assistente quando você seleciona o arquivo.  
  
         Se a fonte for um provedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)], você também poderá usar a opção para copiar resultados da consulta, fornecendo a cadeia DBCommand como a consulta.  
  
         Se a fonte de dados é um modo de exibição, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de importação e exportação converte automaticamente o modo de exibição em uma tabela no destino.  
  
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
  
     Se o assistente for iniciado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no prompt de comando, o pacote poderá ser executado imediatamente. Você também pode salvar o pacote para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** banco de dados ou o sistema de arquivos. Para obter mais informações sobre o **msdb** banco de dados, consulte [pacote de gerenciamento &#40;SSIS Service&#41;](../service/package-management-ssis-service.md).  
  
     Ao salvar o pacote, você poder definir o nível de proteção do pacote e, se esse nível de proteção usar uma senha, fornecer a senha. Para obter mais informações sobre níveis de proteção do pacote, consulte [controle de acesso de dados confidenciais em pacotes](../security/access-control-for-sensitive-data-in-packages.md).  
  
     Se o assistente é iniciado de um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] project no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você não pode executar o pacote do assistente. Em vez disso, o pacote será adicionado ao projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir do qual você iniciou o assistente. Você pode executar o pacote [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
    > [!NOTE]  
    >  Em [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a opção para salvar o pacote criado pelo assistente não está disponível.  
  
## <a name="see-also"></a>Consulte também  
 [Assistente de exportação e importação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [Criar pacotes nas Ferramentas de Dados do SQL Server](../create-packages-in-sql-server-data-tools.md)  
  
  