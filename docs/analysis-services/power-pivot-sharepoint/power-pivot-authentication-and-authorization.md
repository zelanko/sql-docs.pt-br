---
title: Power Pivot Authentication and Authorization | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40b36877a7c64c10fb2eee2933b1ac2461719c0c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-authentication-and-authorization"></a>Autenticação e autorização do Power Pivot
  Uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, executada dentro de um farm do SharePoint 2010, usa o subsistema de autenticação e o modelo de autorização fornecidos pelos servidores do SharePoint. A infraestrutura de segurança do SharePoint se estende ao conteúdo e às operações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] porque todo o conteúdo relacionado ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]é armazenado nos bancos de dados de conteúdo do SharePoint, e todas as operações relacionadas ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]são executadas pelos serviços compartilhados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Os usuários que solicitam uma pasta de trabalho que contém dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são autenticados, usando uma identidade de usuário do SharePoint que é baseada na respectiva identidade de usuário do Windows. As permissões de exibição na pasta de trabalho determinam se a solicitação é concedida ou negada.  
  
 Como a integração com os Serviços do Excel é necessária para análises de dados de autoatendimento, a proteção de um servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] exige que você também compreenda a segurança dos Serviços do Excel. Quando um usuário consulta um Tabela Dinâmica que tem uma conexão de dados a dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , os Serviços do Excel encaminham uma solicitação de conexão de dados a um servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm para carregar os dados. Essa interação entre os servidores exige que você compreenda como configurar parâmetros de segurança para ambos os servidores.  
  
 Clique nos links a seguir para ler seções específicas deste tópico:  
  
 [Autenticação do Windows usando o requisito de logon do modo clássico](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Operações do Power Pivot que exigem autorização do usuário](#UserConnections)  
  
 [Permissões do SharePoint para acesso aos dados do Power Pivot](#Permissions)  
  
 [Considerações de segurança dos Serviços do Excel para pastas de trabalho do Power Pivot](#excel)  
  
##  <a name="bkmk_auth"></a> Autenticação do Windows usando o requisito de logon do modo clássico  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint dá suporte a um conjunto reduzido das opções de autenticação que estão disponíveis no SharePoint. Das opções de autenticação disponíveis, somente autenticação do Windows tem suporte para uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Além disso, o aplicativo Web pelo qual o logon ocorre deve ser configurado para o modo clássico.  
  
 A autenticação do Windows é exigida porque o mecanismo de dados do Analysis Services em uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint só dá suporte à autenticação do Windows. Os serviços do Excel estabelecem conexões com o Analysis Services pelo provedor do OLE DB de MSOLAP usando uma identidade de usuário do Windows que foi autenticada por NTLM ou o protocolo Kerberos.  
  
 O segundo requisito, a autenticação de modo clássica no aplicativo Web, é exigido para assegurar o operabilidade do serviço Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O serviço Web é um componente executado em um front-end da Web e fornece redirecionamento HTTP para o servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no farm. Enquanto o serviço Web tem reconhecimento de declaração para comunicações entre serviços, não tem reconhecimento de declaração para as solicitações de conexão de dados que ele roteia para um serviço compartilhado do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. As solicitações para carregar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] têm suporte somente para conexões autenticadas que vêm do IIS usando uma identidade do Windows. A entrada em modo clássico no aplicativo Web é o que habilita uma conexão bem-sucedida do serviço Web do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para os serviços compartilhados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
 Embora a entrada em modo clássico não seja necessária para o cenário mais comum de acesso a dados (em que os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são extraídos da mesma pasta de trabalho do Excel que os renderiza), não tente usar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint com aplicativos Web do SharePoint configurados para usar outros provedores de autenticação. Se isso for feito, o resultado será uma falha na conexão sempre que os usuários tentarem conectar pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como uma fonte de dados externa.  
  
 Sem a entrada em modo clássico, os seguintes tipos de solicitações tratados pelo serviço Web do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] falharão:  
  
-   Qualquer solicitação de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] originada fora do farm (por exemplo, criação de um relatório no Designer de Relatórios ou no Construtor de Relatórios, em que a fonte de dados é uma URL do SharePoint para uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] )  
  
-   Solicitações no farm de um aplicativo cliente ou relatório que use a pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como uma fonte de dados externa (por exemplo, criação de uma pasta de trabalho no aplicativo da área de trabalho Excel, usando como fonte de dados uma segunda pasta de trabalho Excel publicada que contém dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] )  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>Como verificar o provedor de autenticação do seu aplicativo  
 Ao criar novos aplicativos Web, selecione a opção **Autenticação de modo clássico** na página Criar Novo Aplicativo Web.  
  
 Para aplicativos Web existentes, use as instruções a seguir para verificar se o aplicativo Web está configurado para usar autenticação do Windows.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos Web**.  
  
2.  Selecione o aplicativo Web.  
  
3.  Clique em **Provedores de autenticação**.  
  
4.  Verifique se você tem um provedor para cada zona, e se a zona Padrão é definida como Windows.  
  
##  <a name="UserConnections"></a> Operações do Power Pivot que exigem autorização do usuário  
 A autorização do SharePoint é usada exclusivamente para todos os níveis de acesso à consulta do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e ao processamento de dados.  
  
 O modelo de autorização baseado em funções do Analysis Services não tem suporte. Não há nenhuma autorização baseada em função para os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no nível de célula, linha ou tabela. Você não pode proteger partes diferentes da pasta de trabalho para conceder ou negar acesso a dados confidenciais dentro delas para usuários específicos. Os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] inseridos estão totalmente disponíveis para os usuários que têm permissões de Exibição na pasta de trabalho do Excel em uma biblioteca do SharePoint.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint representará um usuário do SharePoint nos seguintes casos:  
  
-   Consultas a Tabelas Dinâmicas ou Gráficos Dinâmicos que têm conexões de dados com um banco de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , onde um aplicativo do serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] estabelece conexões em nome de um usuário com uma instância do serviço compartilhado do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] específica que processa os dados.  
  
-   Carregando dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do cache ou de uma biblioteca se os dados não estiverem disponíveis de outra maneira. Se uma solicitação de conexão de dados for feita para dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que ainda não estão carregados no sistema, a instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] usará a identidade do usuário do SharePoint para recuperar a fonte de dados de uma biblioteca de conteúdo e carregá-la na memória.  
  
-   Operações de atualização de dados que salvam uma cópia atualizada da fonte de dados na pasta de trabalho em uma biblioteca de conteúdo. Neste caso, um log real em operação é executado usando o nome de usuário e a senha que são recuperados de um aplicativo de destino no Serviço de Repositório Seguro. As credenciais podem ser a conta autônoma de atualização de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou credenciais que foram armazenadas com a agenda de atualização de dados quando ela foi criada. Para saber mais, consulte [Configurar credenciais armazenadas para Power Pivot para atualização de dados (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75) e [Configurar a conta autônoma de atualização de dados do Power Pivot (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493).  
  
##  <a name="Permissions"></a> Permissões do SharePoint para acesso aos dados do Power Pivot  
 A publicação, gerenciamento e proteção de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] têm suporte apenas por meio da integração do SharePoint. Os servidores do SharePoint fornecem subsistemas de autenticação e autorização que garantem acesso legítimo aos dados. Não há qualquer cenário com suporte para implantar uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de maneira segura fora de um farm do SharePoint.  
  
 O acesso do usuário a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é somente leitura no servidor por meio de permissões de Exibição ou mais altas. Permissões de colaboração permitem adicionar e editar o arquivo. As alterações aos dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] exigem que você baixe a pasta de trabalho para um aplicativo de área de trabalho do Excel que tenha o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel instalado. As permissões de colaboração no arquivo determinarão se o usuário pode baixar o arquivo localmente e, em seguida, salvar as alterações novamente no SharePoint.  
  
 Dessa forma, níveis de permissão de Colaboração e Somente Exibição definem o conjunto efetivo de permissões para acesso de usuário aos dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Outros níveis de permissão funcionam na medida em que têm as mesmas permissões que Colaboração e Somente Exibição (por exemplo, como Leitura inclui permissões Somente Exibição, um usuário que receba a permissão de Leitura terá o mesmo nível de acesso que Somente Leitura).  
  
 A tabela a seguir resume os níveis de permissão que determinam o acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e as operações de servidor:  
  
|Nível de permissão|Permite as seguintes tarefas|  
|----------------------|------------------------|  
|Administrador de farm ou serviço|Instalar, habilitar e configurar serviços e aplicativos.<br /><br /> Usar o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e exibir relatórios administrativos.|  
|Controle total|Ativar a integração de recursos do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no nível de conjunto de sites.<br /><br /> Criar uma biblioteca da Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Criar uma biblioteca de feeds de dados.|  
|Contribuir|Adicionar, editar, excluir e baixar as pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Configurar a atualização de dados<br /><br /> Criar novas pastas de trabalho e relatórios com base em pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um site do SharePoint.<br /><br /> Criar documentos de serviço de dados em uma biblioteca de feed de dados|  
|Leitura|Acessar pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como uma fonte de dados externa, em que a URL da pasta de trabalho é inserida explicitamente em uma caixa de diálogo de conexão (por exemplo, no Assistente de Conexão de Dados do Excel).|  
|Exibir Apenas|Exibir pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Exibir o histórico de atualizações de dados.<br /><br /> Conectar uma pasta de trabalho local a uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um site do SharePoint, para adaptar seus dados de outros modos.<br /><br /> Baixar um instantâneo da pasta de trabalho. O instantâneo é uma cópia estática dos dados, sem segmentações de dados, fórmulas ou conexões de dados. O conteúdo do instantâneo é semelhante à cópia de valores de células da janela do navegador.|  
  
##  <a name="excel"></a> Considerações de segurança dos Serviços do Excel para pastas de trabalho do Power Pivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] O processamento de consulta no servidor é estreitamente ligado aos Serviços do Excel. A integração de produto começa no nível do documento, em que pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são arquivos de pasta de trabalho do Excel (.xlsx) que contêm ou fazem referência a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Não há nenhuma extensão de arquivo separada para uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Quando uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é aberta em um site do SharePoint, os Serviços do Excel leem a cadeia de conexão de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] inserida e encaminham a solicitação ao provedor local de OLE DB do SQL Server Analysis Services. Então, o provedor transmite as informações de conexão a um servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Para que as solicitações fluam diretamente entre os dois servidores, os Serviços do Excel devem ser configurados para usar configurações requeridas pelo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
 Nos Serviços do Excel, as configurações relacionadas à segurança são especificadas em locais confiáveis, provedores de dados confiáveis e bibliotecas de conexão de dados confiáveis. A tabela a seguir descreve as configurações que permitem ou aprimoram o acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se uma configuração não estiver listada aqui, ela não terá nenhum efeito nas conexões com o servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para saber como especificar essas configurações passo a passo, consulte a seção "Habilitar Serviços do Excel" em [Configuração inicial (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146).  
  
> [!NOTE]  
>  A maioria das configurações relacionadas à segurança se aplicam a locais confiáveis. Se quiser preservar valores padrão ou usar valores diferentes para sites diferentes, você poderá criar mais um local confiável para sites que contenham dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e, então, configurar os seguintes parâmetros apenas para esse site. Para obter mais informações, consulte [Criar um local confiável para sites do PowerPivot](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
|Área|Configuração|Description|  
|----------|-------------|-----------------|  
|Aplicativo Web|Provedor de autenticação do Windows|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] converte um token de declaração obtido dos Serviços do Excel em uma identidade de usuário do Windows. Qualquer aplicativo Web que utilize os Serviços do Excel como um recurso deve ser configurado para usar o provedor de autenticação do Windows.|  
|Local confiável|Tipo de local|Este valor deve ser definido como **Microsoft SharePoint Foundation**. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recuperam uma cópia do arquivo .xlsx e o carregam em um servidor de Serviços de Análise no farm. O servidor só pode recuperar arquivos .xlsx de uma biblioteca de conteúdo.|  
||Permitir dados externos|Esse valor deve ser definido como **Bibliotecas confiáveis e incorporadas de conexão de dados**. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são inseridas na pasta de trabalho. Se você não permitir conexões inseridas, os usuários poderão exibir o cache de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , mas não poderão interagir com o dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
||Aviso de Atualização|Este valor deverá ser desabilitado se você estiver usando a Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para armazenar pastas de trabalho e relatórios. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] inclui um recurso de visualização de documentos que funciona melhor se a atualização na abertura e a Advertência na Atualização estiverem desabilitados.|  
|Provedores de dados confiáveis|MSOLAP.4<br /><br /> MSOLAP.5|O MSOLAP.4 está incluído por padrão, mas o acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] exige que o provedor de MSOLAP.4 seja a versão SQL Server 2008 R2.<br /><br /> O MSOLAP.5 está instalado com a versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.<br /><br /> Não remova esses provedores da lista de provedores de dados confiáveis. Em alguns casos, você pode precisar instalar cópias adicionais deste provedor em outros servidores do SharePoint em seu farm. Para saber mais, confira [Install the Analysis Services OLE DB Provider on SharePoint Servers](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)(Instalar o provedor OLE DB do Analysis Services em SharePoint Servers).|  
|Bibliotecas de conexão de dados confiáveis|Opcional.|Você pode usar os arquivos da Conexão de Dados do Office (.odc) em pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se você usar arquivos .odc para fornecer informações de conexão a pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] locais, poderá adicionar os mesmos arquivos .odc a essa biblioteca.|  
|Assembly de função definida pelo usuário|Não aplicável.|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ignora os assemblies de funções definidas pelo usuário que você implanta para os Serviços do Excel. Se você confiar em assemblies definidos pelo usuário para um comportamento específico, saiba que o processamento de consultas do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não usará as funções definidas pelo usuário que você criou.|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Configurar o Power Pivot (Power Pivot para SharePoint) da conta de atualização de dados autônoma](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)   
 [Criar um local confiável para sites do PowerPivot](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Arquitetura de segurança do Power Pivot](http://go.microsoft.com/fwlink/?linkID=220970)  
  
  

