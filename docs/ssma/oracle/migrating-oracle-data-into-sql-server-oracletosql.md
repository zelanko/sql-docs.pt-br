---
title: "Migração de dados Oracle no SQL Server (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: e88983497744eef31efd5aa7e27645da7c62b468
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>Migração de dados Oracle no SQL Server (OracleToSQL)
Depois de ter sincronizado com êxito os objetos convertidos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode migrar dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado é o mecanismo de migração de dados do lado do servidor, em seguida, antes de migrar dados, instale o SSMA para os provedores da Oracle no computador que está executando o SSMA e pacote de extensão do Oracle. Também deve estar executando o serviço SQL Server Agent. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalar componentes de servidor (OracleToSQL)](http://msdn.microsoft.com/en-us/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], examine as opções de migração de projeto no **configurações de projeto** caixa de diálogo.  
  
-   Usando essa caixa de diálogo, você pode definir opções, como o tamanho de lote de migração, o bloqueio da tabela, verificação de restrição, manipulação de valor nulo e lidar com valor de identidade. Para obter mais informações sobre as configurações de projeto de migração, consulte [configurações do projeto (migração) (OracleToSQL)](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60).  
  
-   O **mecanismo de migração** no **configurações de projeto** caixa de diálogo permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados:  
  
    1.  Mecanismo de migração de dados do lado cliente  
  
    2.  Mecanismo de migração de dados do lado servidor  
  
**Migração de dados do lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione o **mecanismo de migração de dados do lado do cliente** opção o **configurações de projeto** caixa de diálogo.  
  
-   Em **configurações de projeto**, o **mecanismo de migração de dados do lado do cliente** opção é definida.  
  
    > [!NOTE]  
    > O **mecanismo de migração de dados do lado do cliente** reside dentro do aplicativo do SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados do lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo reside no banco de dados de destino. Ele é instalado por meio do pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes de servidor no SQL Server](http://msdn.microsoft.com/en-us/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
-   Para iniciar a migração no lado do servidor, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
## <a name="migrating-data-to-sql-server"></a>Migração de dados para o SQL Server  
Migração de dados são uma operação de carregamento em massa que move linhas de dados de tabelas do Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tabelas em transações. O número de linhas carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] em cada transação é configurado nas configurações do projeto.  
  
Para exibir mensagens de migração, certifique-se de que o painel de saída está visível. Caso contrário, do **exibição** menu, selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores do Oracle são instalados no computador que está executando o SSMA.  
  
    -   Você sincroniza os objetos convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.  
  
2.  No Gerenciador de metadados do Oracle, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, selecione a caixa de seleção ao lado de **esquemas**.  
  
    -   Para migrar dados ou omitir tabelas individuais, primeiro expanda o esquema, **tabelas**e, em seguida, marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, podem surgir dois casos:  
  
    **Migração de dados do lado do cliente:**  
  
    -   Para executar **a migração de dados do lado do cliente**, selecione o **mecanismo de migração de dados do lado do cliente** opção o **configurações de projeto** caixa de diálogo.  
  
    **Migração de dados do lado do servidor:**  
  
    -   Antes de executar a migração de dados no lado do servidor, certifique-se:  
  
        1.  O SSMA para o pacote de extensão do Oracle está instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
        2.  O serviço SQL Server Agent está em execução na instância do SQL Server.  
  
    -   Para executar **migração de dados do lado do servidor**, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
4.  Clique com botão direito **esquemas** no Gerenciador de metadados do Oracle e clique **migrar dados**. Também é possível migrar dados para objetos individuais ou as categorias de objetos: com o botão direito do objeto ou sua pasta pai; Selecione o **migrar dados** opção.  
  
    > [!NOTE]  
    > Se o SSMA para o pacote de extensão do Oracle não estiver instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]e se **mecanismo de migração de dados do lado do servidor** for selecionado, em seguida, ao migrar os dados para o banco de dados de destino, o seguinte erro: ' componentes de migração de dados do SSMA não foram encontrados no SQL Server, não será possível realizar a migração de dados do servidor. Verifique se o pacote de extensão está instalado corretamente '. Clique em **Cancelar** para finalizar a migração de dados.  
  
5.  No **conectar-se ao Oracle** caixa de diálogo, insira as credenciais de conexão e, em seguida, clique em **conectar**. Para obter mais informações sobre como conectar-se ao Oracle, consulte [conectar-se ao Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)  
  
    Para conectar-se ao banco de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], insira as credenciais de conexão no **conectar ao SQL Server** caixa de diálogo e clique em **conectar**. Para obter mais informações sobre como conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [conectar ao SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    As mensagens serão exibidas no **saída** painel. Quando a migração for concluída, o **relatório de migração de dados** é exibida. Se todos os dados não migrar, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Quando tiver terminado com o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [o relatório de dados de migração (SSMA comuns)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express edition é usado como o banco de dados de destino, é permitida somente cliente lado migração de dados e não há suporte para a migração de dados do lado de servidor.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Oracle para o SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
