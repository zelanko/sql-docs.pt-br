---
title: Habilitar o modo DirectQuery no SSMS | Microsoft Docs
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 544725a89521eb86f61fcfd3194c3d56be9da606
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="enable-directquery-mode-in-ssms"></a>Habilitar o modo DirectQuery no SSMS
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Você pode alterar as propriedades de acesso a dados de um modelo de tabela que já tenha sido implantado, habilitando o modo DirectQuery, em que consultas são executadas em uma fonte de dados relacional de back-end em vez de nos dados em cache residentes na memória.  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as etapas de configuração do DirectQuery diferem de acordo com o nível de compatibilidade do modelo. Veja a seguir etapas que funcionam para todos os níveis de compatibilidade.  
  
 Este artigo pressupõe que você tenha criado e validado um modelo de tabela na memória no nível de compatibilidade 1200 ou superior e somente precisa habilitar o acesso DirectQuery e atualizar as cadeias de conexão. Se você estiver começando de um nível de compatibilidade inferior, precisará atualizá-lo manualmente primeiro. Consulte [Atualizar o Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) para encontrar as etapas.  
  
> [!IMPORTANT]  
>  É recomendável usar o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] em vez do Management Studio para alternar entre modos de armazenamento de dados. Quando você usa o  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para alterar o modelo e depois implantar o servidor, o modelo e o banco de dados permanecem em sincronia. Além disso, alterar os modos de armazenamento no modelo permite que você verifique os erros de validação que ocorrem. Ao usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conforme a descrição neste artigo, os erros de validação não são relatados.  
  
## <a name="requirements"></a>Requisitos  
 Habilitar o uso do modo DirectQuery em um modelo de tabela é um processo de várias etapas:  
  
-   Certifique-se de que o modelo não tenha recursos que possam causar erros de validação no modo DirectQuery e altere o modo de armazenamento de dados no modelo de na memória para DirectQuery.  
  
     Uma lista de restrições de recursos está documentada em [o modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).  
  
-   Examine a cadeia de conexão e as credenciais usadas pelo banco de dados implantado para recuperar dados do banco de dados externo de back-end. Certifique-se de que haja apenas uma conexão e que as configurações sejam adequadas para a execução da consulta.  
  
     Bancos de dados de tabela que não foram projetados especificamente para DirectQuery podem ter várias conexões que agora precisam ser reduzidas a uma, conforme é exigido para o modo DirectQuery.  
  
     As credenciais usadas originalmente para processar dados agora serão usadas para consultar dados. Como parte da configuração do DirectQuery, verifique e possivelmente altere a conta se você usar números diferentes para operações dedicadas.  
  
     O modo DirectQuery é o único cenário no qual o Analysis Services executa delegação confiável. Se sua solução requer delegação obter resultados de consultas específicas de usuários, a conta usada para conectar-se ao banco de dados back-end deve ter permissão para delegar a identidade do usuário que fez a solicitação e as identidades de usuário devem ter permissões de leitura no banco de dados back-end.  
  
-   A última etapa é confirmar se o modo Consulta Direta está operacional por meio da execução de uma consulta.  
  
## <a name="step-1-check-the-compatibility-level"></a>Etapa 1: Verificar o nível de compatibilidade  
 As propriedades que definem o acesso aos dados são diferentes de acordo com os níveis de compatibilidade. Uma etapa preliminar é verificar o nível de compatibilidade do banco de dados.  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], conecte-se à instância que tem o modelo de tabela.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados > **Propriedades** > **Nível de Compatibilidade**.  
  
     O valor será **SQL Server 2016 (1200)** ou um nível anterior como **SQL Server 2012 SP1 ou posterior (1103)**. Na próxima etapa, siga as instruções que são válidas para o nível de compatibilidade em questão.  
  
 Quando você altera um modelo de tabela para o modo DirectQuery, o novo modo de armazenamento de dados entra em vigor imediatamente.  
  
## <a name="step-2a-switch-a-tabular-1200-database-to-directquery-mode"></a>Etapa 2a: Mudar um banco de dados de tabela 1200 para o modo DirectQuery  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados > **Propriedades** > **Modelo** > **Modo Padrão**.  
  
2.  Defina o modo como **DirectQuery**.  
  
    |||  
    |-|-|  
    |**Valores válidos**|**Descrição**|  
    |**DirectQuery**|Consultas são executadas em um banco de dados relacional back-end, usando a conexão da fonte de dados definida para o modelo.<br /><br /> Consultas ao modelo são convertidas em consultas de banco de dados nativo e redirecionadas para a fonte de dados.<br /><br /> Quando você processa um modelo definido para o modo DirectQuery, somente metadados são compilados e implantados. Os dados em si são externos ao modelo, residindo nos arquivos de banco de dados da fonte de dados em funcionamento.|  
    |**Importar**|Consultas são executadas no banco de dados de tabela em MDX ou DAX.<br /><br /> Quando você processa um modelo definido para modo de Importação, os dados são recuperados de uma fonte de dados back-end e armazenados em disco. Quando o banco de dados é carregado, os dados são copiados totalmente para a memória para tornar verificações e consultas de tabela muito mais rápidas.<br /><br /> Esse é o modo padrão para modelos de tabela e é o único modo para certas fontes de dados (não relacionais).|  
  
## <a name="step-2b-switch-a-tabular-1100-1103-database-to-directquery-mode"></a>Etapa 2b: Mudar um banco de dados de tabela 1100-1103 para o modo DirectQuery  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados > **Propriedades** > **Banco de Dados** > **DirectQueryMode**.  
  
2.  Defina o modo como **DirectQuery**.  
  
     As propriedades do modo Padrão são:  
  
    |||  
    |-|-|  
    |**Valores válidos**|**Descrição**|  
    |**InMemory**|Consultas usam somente os dados armazenados em cache, na memória.|  
    |**InMemorywithDirectQuery**|As consultas usam o cache por padrão, a menos que especificado em contrário na cadeia de conexão do cliente.<br /><br /> Esse é um modo híbrido, onde as partições são individualmente configuradas para serem usadas na memória ou no DirectQuery.|  
    |**DirectQuery**|As consultas só usam a fonte de dados relacional.|  
    |**DirectQuerywithInMemory**|As consultas usam a fonte de dados relacional por padrão, a menos que especificado em contrário na cadeia de conexão do cliente.<br /><br /> Esse é um modo híbrido, onde as partições são individualmente configuradas para serem usadas na memória ou no DirectQuery.|  
  
 **Armazenamento de Dados Híbrido**  
  
 Ao usar a combinação de acesso baseado em disco e na memória, o cache ainda fica disponível e pode ser usado para consultas. Um modo híbrido oferece várias opções:  
  
-   Quando o cache e a fonte de dados relacional estão disponíveis, você pode definir o método de conexão preferencial, mas é o cliente quem controla a fonte a ser usada, usando a propriedade de cadeia de conexão do DirectQueryMode.  
  
-   Você pode configurar partições no cache de modo que a partição primária usada no modo DirectQuery nunca seja processada e sempre faça referência à fonte relacional. Há muitas formas de usar partições para otimizar o design de modelo e a experiência de relatórios. Para obter mais informações, consulte [definir partições em modelos DirectQuery](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md).  
  
-   Após a implantação do modelo, você pode alterar o método de conexão preferencial. Por exemplo, você pode usar um modo híbrido para testes e alternar o modelo para **apenas DirectQuery** somente depois de testar bem relatórios ou consultas que usam o modelo. Para obter mais informações, consulte [Definir ou alterar o método de conexão preferencial para DirectQuery](http://msdn.microsoft.com/library/f10d5678-d678-4251-8cce-4e30cfe15751).  
  
## <a name="step-3-check-the-connection-properties-on-the-database"></a>Etapa 3: Verificar as propriedades de conexão do banco de dados  
 Dependendo de como a conexão da fonte de dados seja configurada, alternar para o modo DirectQuery pode alterar o contexto de segurança da conexão. Ao alterar o modo de acesso de dados, examine as propriedades da cadeia de conexão e de representação para verificar se o logon é válido para conexões contínuas com o banco de dados de back-end.  
  
 Examine a seção **Configurar o Analysis Services para delegação confiável** em [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) para obter informações básicas sobre a delegação de uma identidade de usuário para cenários de DirectQuery.  
  
1.  No Pesquisador de Objetos, expanda **Conexões** e clique duas vezes em uma conexão para exibir suas propriedades.  
  
     Para modelos DirectQuery, deve haver apenas uma conexão definida para o banco de dados e a fonte de dados deve ser relacional e de um tipo de banco de dados compatível. Consulte [fontes de dados suportadas](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md).  
  
2.  **A cadeia de conexão** deve especificar o servidor, o nome do banco de dados e o método de autenticação usado em operações de DirectQuery. Se você estiver usando a autenticação do SQL Server, pode especificar aqui o login do banco de dados.  
  
3.  **Informações sobre Representação** são usadas para a autenticação do Windows. Opções válidas para modelos de tabela no modo DirectQuery incluem:  
  
    -   **Usar a conta de serviço**. Você pode escolher essa opção se a conta de serviço do Analysis Services tiver permissões de leitura no banco de dados relacional.  
  
    -   **Usar nome de usuário e senha específicos**. Especifique uma conta de usuário do Windows que tenha permissões de leitura no banco de dados relacional.  
  
 Observe que estas credenciais são usadas apenas para responder consultas no repositório de dados relacional; elas não são iguais às credenciais usadas para processar o cache de um modelo híbrido.  
  
 A representação não pode ser usada quando o modelo é usado apenas na memória. A configuração **ImpersonateCurrentUser**é inválida, a menos que o modelo esteja usando o modo DirectQuery.  
  
## <a name="step-4-validate-directquery-access"></a>Etapa 4: Validar o acesso do DirectQuery  
  
1.  Inicie um rastreamento usando o SQL Server Profiler ou xEvents no Management Studio, conectado ao banco de dados relacional no SQL Server.  
  
     Se você estiver usando Oracle ou Teradata, use as ferramentas de rastreamento para essas plataformas de banco de dados.  
  
2.  No Management Studio, digite e execute uma consulta MDX simples, como `select <some measure> on 0 from model.`.  
  
3.  No rastreamento, você deve ver evidências de execução de consultas no banco de dados relacional.  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Fontes de dados com suporte](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [Monitorar uma instância do Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  
