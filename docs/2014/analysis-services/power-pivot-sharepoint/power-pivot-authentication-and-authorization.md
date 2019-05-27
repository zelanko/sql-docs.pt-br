---
title: PowerPivot Authentication and Authorization | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2fe19165a8b9e0d419a1cba67eeb4ada6a3ce183
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071427"
---
# <a name="powerpivot-authentication-and-authorization"></a>Autenticação e autorização PowerPivot
  Uma implantação do PowerPivot para SharePoint, executada dentro de um farm do SharePoint 2010, usa o subsistema de autenticação e o modelo de autorização fornecidos pelos servidores do SharePoint. A infraestrutura de segurança do SharePoint se estende ao conteúdo e operações do PowerPivot porque todo o conteúdo relacionado ao PowerPivot é armazenado nos bancos de dados de conteúdo do SharePoint, e todas as operações relacionadas ao PowerPivot é executado pelos serviços compartilhados PowerPivot no farm. Os usuários que solicitam uma pasta de trabalho que contém dados PowerPivot são autenticados, usando uma identidade de usuário do SharePoint que é baseada na respectiva identidade de usuário do Windows. As permissões de exibição na pasta de trabalho determinam se a solicitação é concedida ou negada.  
  
 Como a integração com os Serviços do Excel é necessária para análises de dados de autoatendimento, a proteção de um servidor do PowerPivot exige que você também compreenda a segurança dos Serviços do Excel. Quando um usuário consulta um Tabela Dinâmica que tem uma conexão de dados a dados PowerPivot, os Serviços do Excel encaminham uma solicitação de conexão de dados a um servidor do PowerPivot no farm para carregar os dados. Essa interação entre os servidores exige que você compreenda como configurar parâmetros de segurança para ambos os servidores.  
  
 Clique nos links a seguir para ler seções específicas deste tópico:  
  
 [Autenticação do Windows usando o requisito de logon do modo clássico](power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Operações do PowerPivot que exigem autorização do usuário](#UserConnections)  
  
 [Permissões do SharePoint para acesso a dados PowerPivot](#Permissions)  
  
 [Considerações de segurança de serviços do Excel para pastas de trabalho PowerPivot](#excel)  
  
##  <a name="bkmk_auth"></a> Autenticação do Windows usando o requisito de logon do modo clássico  
 O PowerPivot para SharePoint dá suporte a um conjunto reduzido das opções de autenticação que estão disponíveis no SharePoint. Das opções de autenticação disponíveis, somente autenticação do Windows tem suporte para uma implantação do PowerPivot para SharePoint. Além disso, o aplicativo Web pelo qual o logon ocorre deve ser configurado para o modo clássico.  
  
 A autenticação do Windows é exigida porque o mecanismo de dados do Analysis Services em uma implantação do PowerPivot para SharePoint só dá suporte à autenticação do Windows. Os serviços do Excel estabelecem conexões com o Analysis Services pelo provedor do OLE DB de MSOLAP usando uma identidade de usuário do Windows que foi autenticada por NTLM ou o protocolo Kerberos.  
  
 O segundo requisito, a autenticação de modo clássica no aplicativo Web, é exigido para assegurar o operabilidade do serviço Web PowerPivot. O serviço Web é um componente executado em um front-end da Web e fornece redirecionamento HTTP para o servidor do PowerPivot para SharePoint no farm. Enquanto o serviço Web tem reconhecimento de declaração para comunicações entre serviços, não tem reconhecimento de declaração para as solicitações de conexão de dados que ele roteia para um serviço compartilhado do PowerPivot no farm. As solicitações para carregar dados PowerPivot têm suporte somente para conexões autenticadas que vêm do IIS usando uma identidade do Windows. O logon em modo clássico no aplicativo Web é o que habilita uma conexão bem-sucedida do serviço Web PowerPivot para os serviços compartilhados PowerPivot no farm.  
  
 Embora o logon em modo clássico não seja necessário para o cenário mais comum de acesso a dados (onde os dados PowerPivot são extraídos da mesma pasta de trabalho do Excel que os renderiza), não tente usar o PowerPivot para SharePoint com aplicativos Web do SharePoint configurados para usar outros provedores de autenticação. Se isso for feito, o resultado será uma falha na conexão sempre que os usuários tentarem conectar pastas de trabalho PowerPivot como uma fonte de dados externa.  
  
 Sem o logon do modo clássico, os seguintes tipos de solicitações que são tratados pelo serviço Web PowerPivot falharão:  
  
-   Qualquer solicitação de dados PowerPivot originada fora do farm (por exemplo, criação de um relatório no Designer de Relatórios ou no Construtor de Relatórios, em que a fonte de dados é uma URL do SharePoint URL para uma pasta de trabalho PowerPivot)  
  
-   Solicitações no farm de um aplicativo cliente ou relatório que use a pasta de trabalho PowerPivot como uma fonte de dados externa (por exemplo, criação de uma pasta de trabalho no aplicativo desktop Excel, usando como fonte de dados uma segunda pasta de trabalho Excel publicada que contém dados PowerPivot)  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>Como verificar o provedor de autenticação do seu aplicativo  
 Ao criar novos aplicativos Web, selecione a opção **Autenticação de modo clássico** na página Criar Novo Aplicativo Web.  
  
 Para aplicativos Web existentes, use as instruções a seguir para verificar se o aplicativo Web está configurado para usar autenticação do Windows.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos Web**.  
  
2.  Selecione o aplicativo Web.  
  
3.  Clique em **Provedores de autenticação**.  
  
4.  Verifique se você tem um provedor para cada zona, e se a zona Padrão é definida como Windows.  
  
##  <a name="UserConnections"></a> Operações do PowerPivot que exigem autorização do usuário  
 A autorização do SharePoint é usada exclusivamente para todos os níveis de acesso à consulta do PowerPivot e ao processamento de dados.  
  
 O modelo de autorização baseado em funções do Analysis Services não tem suporte. Não há nenhuma autorização baseada em função para os dados PowerPivot no nível de célula, linha ou tabela. Você não pode proteger partes diferentes da pasta de trabalho para conceder ou negar acesso a dados confidenciais dentro delas para usuários específicos. Os dados PowerPivot inseridos estão totalmente disponíveis para os usuários que têm permissões de Exibição na pasta de trabalho do Excel em uma biblioteca do SharePoint.  
  
 O PowerPivot para SharePoint representará um usuário do SharePoint nos seguintes casos:  
  
-   Consultas a Tabelas Dinâmicas ou Gráficos Dinâmicos que têm conexões de dados com um banco de dados PowerPivot, onde um aplicativo do serviço PowerPivot estabelece conexões em nome de um usuário com uma instância do serviço compartilhado PowerPivot específica que processa os dados.  
  
-   Carregando dados PowerPivot do cache ou de uma biblioteca se os dados não estiverem disponíveis de outra maneira. Se uma solicitação de conexão de dados for feita para dados PowerPivot que ainda não estão carregados no sistema, a instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] usará a identidade do usuário do SharePoint para recuperar a fonte de dados de uma biblioteca de conteúdo e carregá-la na memória.  
  
-   Operações de atualização de dados que salvam uma cópia atualizada da fonte de dados na pasta de trabalho em uma biblioteca de conteúdo. Neste caso, um log real em operação é executado usando o nome de usuário e a senha que são recuperados de um aplicativo de destino no Serviço de Repositório Seguro. As credenciais podem ser a conta autônoma de atualização de dados PowerPivot ou credenciais que foram armazenadas com a agenda de atualização de dados quando ela foi criada. Para obter mais informações, consulte [configurar credenciais armazenadas para atualização de dados do PowerPivot do &#40;PowerPivot para SharePoint&#41; ](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md) e [configurar o PowerPivot conta autônoma de dados de atualização &#40; O PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
##  <a name="Permissions"></a> Permissões do SharePoint para acesso a dados PowerPivot  
 A publicação, gerenciamento e proteção de uma pasta de trabalho PowerPivot têm suporte apenas por meio da integração do SharePoint. Os servidores do SharePoint fornecem subsistemas de autenticação e autorização que garantem acesso legítimo aos dados. Não há nenhum cenário com suporte para implantar uma pasta de trabalho PowerPivot de maneira segura fora de um farm do SharePoint.  
  
 O acesso do usuário a dados PowerPivot é somente leitura no servidor por meio de permissões de Exibição ou mais altas. Permissões de colaboração permitem adicionar e editar o arquivo. As alterações aos dados PowerPivot exigem que você baixe a pasta de trabalho para um aplicativo de área de trabalho do Excel que tenha o PowerPivot para Excel instalado. As permissões de colaboração no arquivo determinarão se o usuário pode baixar o arquivo localmente e, em seguida, salvar as alterações novamente no SharePoint.  
  
 Dessa forma, níveis de permissão de Colaboração e Somente Exibição definem o conjunto efetivo de permissões para acesso de usuário aos dados PowerPivot. Outros níveis de permissão funcionam na medida em que têm as mesmas permissões que Colaboração e Somente Exibição (por exemplo, como Leitura inclui permissões Somente Exibição, um usuário que receba a permissão de Leitura terá o mesmo nível de acesso que Somente Leitura).  
  
 A tabela a seguir resume os níveis de permissão que determinam acesso a dados PowerPivot e as operações de servidor:  
  
|Nível de permissão|Permite as seguintes tarefas|  
|----------------------|------------------------|  
|Administrador de farm ou serviço|Instalar, habilitar e configurar serviços e aplicativos.<br /><br /> usar o Painel de Gerenciamento do PowerPivot e exibir relatórios administrativos.|  
|Controle total|Ativar a integração de recursos do PowerPivot em nível de conjunto de sites.<br /><br /> Criar uma biblioteca da Galeria do PowerPivot<br /><br /> Criar uma biblioteca de feeds de dados.|  
|Contribuir|Adicionar, editar, excluir e baixar pastas de trabalho PowerPivot.<br /><br /> Configurar a atualização de dados<br /><br /> Criar novas pastas de trabalho e novos relatórios com base em pastas de trabalho PowerPivot em um site do SharePoint.<br /><br /> Criar documentos de serviço de dados em uma biblioteca de feed de dados|  
|leitura|Acesse pastas de trabalho PowerPivot como uma fonte de dados externa, em que a URL da pasta de trabalho é inserida explicitamente em uma caixa de diálogo de conexão (por exemplo, no Assistente de Conexão de dados do Excel).|  
|Exibir Apenas|Exibir pastas de trabalho PowerPivot.<br /><br /> Exibir o histórico de atualizações de dados.<br /><br /> Conectar uma pasta de trabalho local a uma pasta de trabalho PowerPivot em um site do SharePoint, para adaptar seus dados de outros modos.<br /><br /> Baixar um instantâneo da pasta de trabalho. O instantâneo é uma cópia estática dos dados, sem segmentações de dados, fórmulas ou conexões de dados. O conteúdo do instantâneo é semelhante à cópia de valores de células da janela do navegador.|  
  
##  <a name="excel"></a> Considerações de segurança de serviços do Excel para pastas de trabalho PowerPivot  
 O processamento de consulta do PowerPivot no servidor é estreitamente ligado aos serviços do Excel. A integração de produto começa no nível do documento, em que pastas de trabalho PowerPivot são arquivos de pasta de trabalho do Excel (.xlsx) que contêm ou referenciam dados PowerPivot. Não há nenhuma extensão de arquivo separada para uma pasta de trabalho PowerPivot.  
  
 Quando uma pasta de trabalho PowerPivot é aberta em um site do SharePoint, os Serviços do Excel leem a cadeia de conexão de dados PowerPivot inserida e encaminham a solicitação ao provedor local de OLE DB do SQL Server Analysis Services. Então, o provedor transmite as informações de conexão a um servidor do PowerPivot no farm. Para que as solicitações fluam diretamente entre os dois servidores, os Serviços do Excel devem ser configurados para usar configurações requeridas pelo PowerPivot para SharePoint.  
  
 Nos Serviços do Excel, as configurações relacionadas à segurança são especificadas em locais confiáveis, provedores de dados confiáveis e bibliotecas de conexão de dados confiáveis. A tabela a seguir descreve as configurações que permitem ou aprimoram o acesso a dados PowerPivot. Se uma configuração não estiver listada aqui, ela não terá nenhum efeito nas conexões com o servidor do PowerPivot. Para obter instruções sobre como especificar essas configurações passo a passo, consulte a seção "Ativar serviços do Excel" em [a configuração inicial &#40;PowerPivot para SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).  
  
> [!NOTE]  
>  A maioria das configurações relacionadas à segurança se aplicam a locais confiáveis. Se quiser preservar valores padrão ou usar valores diferentes para sites diferentes, você poderá criar mais um local confiável para sites que contenham dados PowerPivot e, então, configurar os seguintes parâmetros apenas para esse site. Para obter mais informações, consulte [criar um local confiável para sites do PowerPivot na Administração Central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
|Área|Configuração|Descrição|  
|----------|-------------|-----------------|  
|Aplicativo Web|Provedor de autenticação do Windows|O PowerPivot converte um token de declaração obtido dos Serviços do Excel em uma identidade de usuário do Windows. Qualquer aplicativo Web que utilize os Serviços do Excel como um recurso deve ser configurado para usar o provedor de autenticação do Windows.|  
|Local confiável|Tipo de local|Este valor deve ser definido como **Microsoft SharePoint Foundation**. Os servidores do PowerPivot recuperam uma cópia do arquivo .xlsx e o carregam em um servidor de Serviços de Análise no farm. O servidor só pode recuperar arquivos .xlsx de uma biblioteca de conteúdo.|  
||Permitir dados externos|Esse valor deve ser definido como **Bibliotecas confiáveis e incorporadas de conexão de dados**. As conexões de dados PowerPivot são inseridas na pasta de trabalho. Se você não permitir conexões inseridas, os usuários poderão exibir o cache de Tabela Dinâmica, mas não poderão interagir com o dados PowerPivot.|  
||Aviso de Atualização|Este valor deverá ser desabilitado se você estiver usando a Galeria do PowerPivot para armazenar pastas de trabalho e relatórios. A Galeria do PowerPivot inclui um recurso de visualização de documentos que funciona melhor se a atualização na abertura e a Advertência na Atualização estiverem desabilitados.|  
|Provedores de dados confiáveis|MSOLAP.4<br /><br /> MSOLAP.5|O MSOLAP.4 está incluído por padrão, mas o acesso a dados PowerPivot exige que o provedor de MSOLAP.4 seja a versão SQL Server 2008 R2.<br /><br /> O MSOLAP.5 está instalado com a versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do PowerPivot para SharePoint.<br /><br /> Não remova esses provedores da lista de provedores de dados confiáveis. Em alguns casos, você pode precisar instalar cópias adicionais deste provedor em outros servidores do SharePoint em seu farm. Para saber mais, confira [Install the Analysis Services OLE DB Provider on SharePoint Servers](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)(Instalar o provedor OLE DB do Analysis Services em SharePoint Servers).|  
|Bibliotecas de conexão de dados confiáveis|Opcional.|Você pode usar arquivos .odc em pastas de trabalho PowerPivot. Se você usar arquivos .odc para fornecer informações de conexão a pastas de trabalho PowerPivot locais, poderá adicionar os mesmos arquivos .odc a essa biblioteca.|  
|Assembly de função definida pelo usuário|Não aplicável.|O PowerPivot para SharePoint ignora os assemblies de funções definidas pelo usuário que você cria para os Serviços do Excel. Se você confiar em assemblies definidos pelo usuário para um comportamento específico, saiba que o processamento de consultas do PowerPivot não usará as funções definidas pelo usuário que você criou.|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço PowerPivot](configure-power-pivot-service-accounts.md)   
 [Configurar o PowerPivot conta de atualização de dados autônoma &#40;PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [Criar um local confiável para sites do PowerPivot na Administração Central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Arquitetura de segurança do PowerPivot](https://go.microsoft.com/fwlink/?linkID=220970)  
  
  
