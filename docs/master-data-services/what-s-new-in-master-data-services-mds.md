---
title: Novidades no MDS (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 07/08/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ad530f60-d480-4457-ba7a-93a10c8a1695
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: aaa80c3b66d7991414033c9c05c79b12681d4ef4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488038"
---
# <a name="what39s-new-in-master-data-services-mds"></a>Novidades no MDS (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico resume as alterações e atualizações na versão [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. 
  
 Para obter uma visão geral de como organizar dados no [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], veja [Visão geral do Master Data Services](../master-data-services/master-data-services-overview-mds.md). 
  
 **Para instalar o Master Data Services, configure o Site e o banco de dados e implante os modelos de exemplo, veja** [Visão Geral do Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md).  
  
 **Download**  
  
-   Para baixar o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], acesse o  **[Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**.  
  
-   Tem uma conta do Azure?  Então, acesse **[aqui](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** para executar uma máquina virtual com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] já instalado.  
  
##  <a name="improved-performance"></a>Desempenho aprimorado  
  
 As melhorias de desempenho permitem a você criar modelos mais amplos, carregar dados com mais eficiência e obter melhor desempenho geral. Isso inclui melhoria de desempenho do suplemento para o Microsoft Excel com o intuito de diminuir os tempos de carregamento e habilitar o suplemento para lidar com entidades maiores.  
  
 Para saber mais sobre o suplemento do Microsoft Excel, confira [Suplemento do Master Data Services para Microsoft Excel](../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md).  
  
 Veja a seguir as melhorias de recurso incluídas.  
  
-   Há compactação de dados no nível de entidade, que está habilitada por padrão. Quando a compactação de dados está habilitada, todos os índices e tabelas relacionados à entidade são compactados com a compactação no Nível de Linha do SQL. Isso reduz significativamente a E/S de disco na leitura ou na atualização dos dados mestre, especialmente quando os dados mestre têm milhões de linhas e/ou muitas colunas de valor NULL.  
  
     Como há um ligeiro aumento no uso da CPU no lado do mecanismo do SQL Server, se você tiver a CPU associada no servidor, será possível desativar a compactação de dados editando a entidade.  
  
     Para saber mais, veja [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)e [Compactação de Dados](../relational-databases/data-compression/data-compression.md).  
  
-   O recurso do IIS, Compactação Dinâmica de Conteúdo, está habilitado, por padrão. Isso reduz consideravelmente o tamanho da resposta xml e salva a E/S de rede, embora o uso da CPU aumente. Se a CPU estiver associada ao servidor, você poderá desativar a compactação de dados adicionando a configuração a seguir ao arquivo Web.config do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
    ```  
    <configuration>  
       \<system.webServer>  
          <urlCompression doStaticCompression="true" doDynamicCompression="false " />  
       \</system.webServer>  
    </configuration>  
  
    ```  
  
     Para saber mais, confira [URL Compression](https://www.iis.net/configreference/system.webserver/urlcompression)(Compactação de URL)  
  
-   Os novos trabalhos do SQL Server Agent a seguir fazem a manutenção de índice e log.  
  
    -   MDS_MDM_Sample_Index_Maintenace  
  
    -   MDS_MDM_Sample_Log_Maintenace  
  
 Por padrão, o trabalho MDS_MDM_Sample_Index_Maintenance é executado semanalmente. É possível modificar o agendamento. Você também pode executar manualmente o trabalho a qualquer momento usando o procedimento armazenado udpDefragmentation. É recomendável executar o procedimento armazenado toda vez que um grande volume de dados mestre é inserido ou atualizado, ou depois que uma nova versão é criada da versão existente.  
  
 Um índice com mais de 30% de fragmentação é recriado online. Durante a recriação, o desempenho é afetado na operação CRUD na mesma tabela. Se a degradação do desempenho for uma preocupação, é recomendável executar o procedimento armazenado fora do horário comercial. Para obter mais informações sobre fragmentação de índice, consulte [Reorganize and Rebuild Indexes](../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Para saber mais, confira essa postagem no Blog do Master Data Services, [Performance and Scale Improvement in SQL Server 2016](https://go.microsoft.com/fwlink/p/?LinkId=615375)(Melhoria de desempenho e escala no SQL Server 2016).  
  
##  <a name="improved-security"></a>Segurança aprimorada  
  
 A nova permissão da função Superusuário dá a um usuário ou grupo as mesmas permissões que o Administrador do Servidor na versão anterior do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. A permissão Superusuário pode ser atribuída a vários usuários e grupos. Na versão anterior, o usuário que originalmente instalava o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] era o administrador do servidor, e era difícil transferir essa permissão a outro usuário ou grupo. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
 Agora um usuário pode receber explicitamente a permissão Administrador no nível de modelo. Isso significa que se, mais tarde, o usuário receber permissões na subárvore do modelo, como no nível de entidade, ele não perderá essa permissão Administrador.  
  
 Nesta versão do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], estamos fornecendo mais níveis de permissões, apresentando as seguintes novas permissões: Ler, Criar, Atualizar e Excluir. Por exemplo, um usuário que tenha somente a permissão Atualizar agora pode atualizar os dados mestre sem criar ou excluir os dados. Quando você concede a um usuário a permissão Criar, Atualizar ou Excluir, o usuário recebe automaticamente a permissão Ler. Você também pode combinar as permissões Ler, Criar, Atualizar e Excluir.  
  
 Quando você atualiza para [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], as permissões antigas são convertidas em novas permissões, conforme mostrado na tabela a seguir.  
  
|Permissão na versão anterior|Nova permissão|  
|------------------------------------|--------------------|  
|O usuário que instala originalmente o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] tem a permissão Administrador do Servidor.|O usuário tem a permissão da função Superusuário|  
|O usuário tem permissões Atualizar no nível de modelo e nenhuma permissão na subárvore do modelo e, portanto, é implicitamente um administrador de modelo.|O usuário tem permissões Administrador explícitas no nível de modelo.|  
|O usuário tem permissões Somente leitura.|O usuário tem permissões Acesso de leitura.|  
|O usuário tem permissões Atualizar.|O usuário tem todas as quatro permissões de acesso: Criar, Atualizar, Excluir e Ler.|  
|O usuário tem permissões Negar.|O usuário tem permissões Negar.|  
  
 Para saber mais sobre permissões, veja [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md).  
  
##  <a name="improved-transaction-log-maintenance"></a>Manutenção do log de transações aprimorada  
  
 Agora você pode limpar os logs de transações em intervalos predeterminados ou agendados usando as configurações do Sistema e no nível de modelo. Para um sistema MDS com muitas alterações de dados e processos ETL, essas tabelas agora podem ser exponencialmente expandidas e gerar degradação de desempenho e problemas de espaço de armazenamento.  
  
 Os tipos de dados a seguir podem ser removidos dos logs.  
  
-   O histórico de transações mais antigo que um número especificado de dias.  
  
-   O histórico de problemas de validação mais antigo que um número especificado de dias.  
  
-   Lotes de preparo que foram executados antes de um número especificado de dias.  
  
 Você pode configurar a frequência em que os dados são removidos dos logs de transações usando as configurações do Sistema e no nível de modelo. Para saber mais, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md) e [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md). Para obter mais informações sobre transações, consulte [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
 O trabalho do SQL Server Agent, MDS_MDM_Sample_Log_Maintenace, aciona a limpeza dos logs de transações e é executado todas as noites. Você pode usar o SQL Server Agent para modificar o agendamento desse trabalho.  
  
 Também é possível chamar procedimentos armazenados para limpar os logs de transações. Para obter mais informações, consulte [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
## <a name="improved-troubleshooting"></a>Solução de problemas aprimorada  
  
 No [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], foram adicionados recursos para melhorar a depuração e facilitar a solução de problemas. Para saber mais, veja [Rastreamento &#40;Master Data Services&#41;](../master-data-services/tracing-master-data-services.md).  
  
## <a name="improved-manageability"></a>Capacidade de gerenciamento aprimorada  
  
 As melhorias na capacidade de gerenciamento ajudam a reduzir os custos de manutenção e afetam positivamente seu ROI (retorno sobre o investimento). Essas melhorias incluem manutenção do log de transações e aprimoramentos na segurança, bem como os recursos novos a seguir.  
  
-   Usar nomes de atributo com mais de 50 caracteres.  
  
-   Renomear e ocultar os atributos Nome e Código.  
  
 Para obter mais informações, consulte os tópicos a seguir.  
  
-   [Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
-   [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  

## <a name="business-rule-improvements"></a>Aperfeiçoamentos da Regra de Negócios
 **Gerenciar regras de negócio (suplemento do MDS para Excel)**  
  
 No suplemento Master Data Services para Excel, você pode gerenciar Regras de Negócio, como criar e editar regras de negócio. As regras de negócio são usadas para validar dados.  
 
 **Extensão das Regras de Negócios**  
  
 Você pode aplicar scripts SQL definidos pelo usuário como uma extensão das ações e condições da regra de negócio. As funções SQL podem ser usadas como uma condição. Os procedimentos armazenados do SQL podem ser usados como uma ação. Para saber mais, veja [Extensão das Regras de Negócios &#40;Master Data Services&#41;](../master-data-services/business-rules-extension-master-data-services.md). 
 
 **Experiência de gerenciamento da regra de negócio reformulada**  
  
 A experiência de gerenciamento de regra de negócio no MDS foi completamente reformulada para melhorar a experiência. Para saber mais sobre esse recurso, veja [Regras de Negócios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md).  
  
 **Funcionalidade de gerenciamento da regra de negócio removida do suplemento MDS para Excel**  
  
 A funcionalidade de gerenciamento Regra de Negócio foi removida do suplemento MDS para Excel porque reformulamos a experiência.    

 **Novas condições da regra de negócio**  
  
 Sete novas condições da regra de negócio foram adicionadas para fornecer um conjunto completo de condições. Para saber mais, veja [Condições de regras de negócios &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md).  

## <a name="derived-hierarchy-improvements"></a>Aprimoramentos da Hierarquia Derivada

 **Relações muitos para muitos em hierarquias derivadas**  
  
 Agora você pode criar uma Hierarquia Derivada que exibe relações muitos para muitos. Uma relação muitos para muitos entre duas entidades pode ser modelada com o uso de uma terceira entidade que fornece um mapeamento entre elas. A entidade de mapeamento é uma entidade que tem dois ou mais atributos baseados em domínio que fazem referência a outras entidades.  
  
 Por exemplo, a entidade M tem um atributo baseado em domínio que faz referência a A e um atributo baseado em domínio que faz referência a B. Você pode criar uma hierarquia de A para B usando a entidade de mapeamento.  
  
 Para mais informações, veja [Mostrar relações muitos para muitos em Hierarquias Derivadas &#40;Master Data Services&#41;](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md)  
 
 **Editar relações muitos para muitos em hierarquias derivadas**  
  
 Você pode editar a relação muitos para muitos modificando os membros da entidade de mapeamento. Para mais informações, veja [Mostrar relações muitos para muitos em Hierarquias Derivadas &#40;Master Data Services&#41;](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md).  
 
 **Experiência aprimorada do gerenciamento da hierarquia derivada**  
  
 A experiência de gerenciamento da hierarquia derivada no MDS foi aprimorada. Para saber mais sobre esse recurso, veja [Criar uma Hierarquia Derivada &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md).  
  
 A funcionalidade de gerenciamento Regra de Negócio foi removida do suplemento MDS para Excel porque reformulamos a experiência.  
 
## <a name="attribute-improvements"></a>Aprimoramentos de Atributos   
    
 **Índices personalizados**  
  
 Você pode criar um índice não clusterizado em um atributo (índice único) ou em uma lista de atributos (índice composto), em uma entidade, para ajudar a melhorar o desempenho da consulta. Para obter mais informações, consulte [Índice personalizado #40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
 
  **Filtros de atributos**  
  
 Para um atributo baseado em domínio, para um membro folha, você pode usar um atributo pai de filtro a fim de restringir os valores permitidos para o atributo baseado em domínio. Para obter mais informações, consulte [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md).  
 
## <a name="entity-and-member-improvements"></a>Aprimoramentos de entidade e membro 
  
 **Relação de Sincronização de Entidade**  
  
 Você pode compartilhar dados entre diferentes modelos criando uma relação de sincronização de entidade. Para saber mais, veja [Relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md).  
  
 **Limpar membros excluídos**  
  
 Agora você pode limpar (excluir permanentemente) todos os membros excluídos temporariamente em uma versão de modelo. Excluir um membro apenas desativa, ou exclui temporariamente, o membro. Para saber mais, veja [Limpar membros da versão &#40;Master Data Services&#41;](../master-data-services/purge-version-members-master-data-services.md).  
 
## <a name="improvements-for-managing-changes"></a>Aprimoramentos para o gerenciamento de alterações 
  
 **Histórico de revisão de membro**  
  
 Um histórico de revisão do membro é registrado quando um membro é alterado. Você pode reverter um histórico de revisão, bem como exibir e anotar as revisões. Usando a propriedade **Dias de Retenção de Log** , você pode especificar por quanto tempo os dados históricos são mantidos. Para saber mais, veja [Reverter histórico de revisões do membro &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md).  
  
 **Conflitos de mesclagem**  
  
 Se você tentar publicar dados que foram alterados por outro usuário, a publicação falhará com um erro de conflito. Para resolver esse erro, você pode executar conflitos de mesclagem e republicar as alterações. Para saber mais, veja [Conflitos de mesclagem (Master Data Services)](../master-data-services/merge-conflicts-master-data-services.md) e [Conflitos de mesclagem (suplemento MDS para Excel)](../master-data-services/microsoft-excel-add-in/merge-conflicts-mds-add-in-for-excel.md).  
  
 **Conjuntos de alterações**  
  
 Você pode usar conjuntos de alterações para salvar alterações pendentes de uma entidade, bem como exibir e modificar as alterações pendentes. Se a entidade exigir aprovação para alterações, você deverá salvar as alterações pendentes em um conjunto de alterações e enviar para aprovação pelo administrador. Para saber mais, veja [Conjuntos de alterações &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md).  
  
 **Gerenciamento e email do conjunto de alterações**  
  
 Nesta versão, você pode exibir e gerenciar todas as alterações por modelo e versão. Também é possível receber notificações por email toda vez que o status do conjunto de alterações mudar para uma entidade que exige aprovação. Para saber mais, veja [Gerenciar conjuntos de alterações &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md) e [Notificações &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md).  
  
 **Exibir e gerenciar o histórico da revisão**  
  
 Você pode exibir e gerenciar o histórico de revisão por entidade e por membro. Se você tiver permissões de atualização, será possível reverter um membro para uma versão anterior. Para saber mais, veja [Reverter histórico de revisões do membro &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md).  
 
## <a name="tool-and-sample-improvements"></a>Aprimoramentos de ferramenta e exemplos 
  
 **Salvar ou abrir arquivos de consulta no suplemento MDS para Excel**  
  
 Na página Gerenciador de Entidades, você pode clicar em **Excel** para salvar os arquivo de consulta de atalho. Ou pode abrir o arquivo de consulta armazenado no computador no suplementos MDS para Excel. O arquivo salvo pode ser aberto usando o aplicativo QueryOpener. Para saber mais, veja [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md).  
  
 O arquivo de consulta contém os filtros e as informações de hierarquia na página do gerenciador.  
   
 **Exemplo de pacotes de implantação de modelo atualizado**  
  
 Os pacotes de exemplo foram atualizados para compatibilidade com novos cenários. Para obter mais informações, confira [Amostras do SQL Server: MDS (Pacotes de Implantação de Modelo)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md).  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
  
## <a name="see-also"></a>Consulte também  
 [Recursos de Master Data Services e Data Quality Services suportados pelas edições do SQL Server 2016](../master-data-services/master-data-services-and-data-quality-services-features-support.md)  
 [Recursos preteridos do Master Data Services](../master-data-services/deprecated-master-data-services-features.md)  
 [Recursos do Master Data Services descontinuados](../master-data-services/discontinued-master-data-services-features.md)
