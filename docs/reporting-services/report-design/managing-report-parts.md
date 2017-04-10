---
title: "Gerenciando partes de relat&#243;rio | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 41947b4c-8ecf-4e4f-b30e-66e1d6692b74
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Gerenciando partes de relat&#243;rio
  Partes de relatório podem ser reutilizadas em relatórios paginados por vários usuários e em vários relatórios. Os usuários podem pesquisar partes de relatório no servidor e adicioná-las a um relatório.  Também podem ser informados de atualizações para a parte de relatório no servidor e republicar novas versões de uma parte de relatório. Essas ações de criação de relatório podem ser afetadas e controladas pelas permissões de segurança dos serviços de relatório.  Este tópico revisa as propriedades de parte de relatório e o comportamento depois que elas estão no servidor.  
  
## Gerenciando partes de relatório  
 Para gerenciar partes de relatório, você pode usar o portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de um servidor de relatório no modo nativo ou páginas do aplicativo de um servidor de relatório no modo integrado do SharePoint.  
  
### Interação e pesquisa do servidor  
 Partes de relatório podem ser publicadas em um servidor de relatório em modo nativo ou em modo integrado do SharePoint. Os usuários podem usar o recurso de galeria de partes de relatório em um aplicativo de criação de relatório, como o Construtor de Relatórios do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para localizar e adicionar partes de relatório a seus relatórios. Quando um usuário pesquisa uma parte de relatório, a pesquisa olha para o catálogo de servidor de relatório independentemente do modo no qual o servidor foi instalado.  
  
 Quando as partes de relatório são publicadas de um aplicativo de criação de relatório, como o Construtor de Relatórios em um servidor de relatório em modo integrado do SharePoint, o catálogo de servidor de relatório também é atualizado e as pesquisas da galeria refletem com precisão a parte de relatório nova ou atualizada.  
  
#### Carregando partes de relatório diretamente para uma pasta do SharePoint  
 Se uma parte de relatório for carregada diretamente em uma pasta de documentos do SharePoint, em vez de publicada de um aplicativo de criação de relatório, o catálogo do servidor de relatório também não será atualizado. As pesquisas da galeria de partes de relatório não localizarão a parte de relatório carregada. Para ajudar a manter suas pastas do SharePoint e o catálogo do servidor de relatório sincronizados, você pode ativar o recurso de sincronização de arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no servidor do SharePoint. Para obter mais informações, consulte [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).  
  
 Os arquivos também podem ser sincronizados usando a chamada de algumas das APIs de gerenciamento de serviços de relatório, como GetProperties e SetProperties.  
  
### Organizando e movendo partes de relatório  
 Planeje com antecedência a maneira como sua equipe usará e organizará partes de relatório, conjuntos de dados compartilhados e fontes de dados compartilhadas. Embora eles possam ser movidos no futuro, poderá haver problemas.  
  
#### Servidor de relatório em modo nativo  
 Se você mover uma parte de relatório em um servidor de relatório em modo nativo para qualquer outra pasta no mesmo servidor, a capacidade de aplicativos de criação para pesquisar ou baixar atualizações da parte de relatório não será afetada. Isto acontece porque o servidor depende do ComponentID exclusivo. No entanto, se a parte de relatório for movida para uma pasta para a qual um usuário não tenha permissões, suas pesquisas não localizarão a parte de relatório e seus relatórios não serão notificados quando houver atualizações na parte de relatório.  
  
#### Servidor de relatório em modo integrado do SharePoint  
 A movimentação de partes de relatório para uma biblioteca ou pasta de documentos diferente tem o mesmo efeito que carregá-las diretamente em um servidor do SharePoint: o catálogo do servidor de relatório não será sincronizado. Para evitar isso, ative o recurso Sincronização de arquivos do Servidor de Relatório no servidor do SharePoint.  
  
 Subpastas são uma exceção. A pesquisa sempre pesquisará subpastas, portanto, se você mover manualmente uma parte de relatório para uma subpasta, ela ainda será localizada em uma pesquisa na galeria de relatórios. ela ainda será localizada em uma pesquisa na galeria de partes de relatório.  
  
### Propriedades do catálogo do servidor de relatório  
 A tabela a seguir descreve como os campos do catálogo do servidor de relatório existentes se relacionam com uma parte de relatório, e com novos campos adicionados ao catálogo de partes de relatório. Eles são expostos no portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], em bibliotecas do SharePoint e em aplicativos de criação de relatório, como o Construtor de Relatórios.  
  
 (*) indica que isso é novo para esta versão.  
  
|Propriedade|Description|Parte de relatório<br /><br /> Critérios de pesquisa de galeria|  
|--------------|-----------------|---------------------------------------------|  
|Nome|Esse é um dos critérios pelos quais um usuário pode pesquisar na Galeria de Partes de Relatório.|Sim|  
|Description|Você deve organizar os nomes de partes de relatório de uma maneira que facilite para os usuários a localização na galeria. Por exemplo, você pode pesquisar pela descrição iniciando com "Vendas>>" para procurar as partes de relatório que envolvem dados e apresentações relacionadas a vendas.|Sim|  
|CreatedBy|A ID do usuário que adicionou originalmente a parte de relatório ao banco de dados do servidor de relatório. O formato exato depende do método de autenticação. Por exemplo, alguns métodos de autenticação mostrarão o domínio\nome de usuário completo nos campos CreatedBy e ModifiedBy.|Sim|  
|CreationDate|As data em que a parte de relatório foi criada originalmente.<br /><br /> Esse é um dos critérios pelos quais um usuário pode pesquisar na Galeria de Partes de Relatório.|Sim|  
|ModifiedBy|ModifiedBy é a ID do usuário que modificou por último a parte do relatório.|Sim|  
|ModifiedDate|A data em que a parte de relatório foi modificada pela última vez no servidor.<br /><br /> Esse campo é usado como parte da lógica para determinar quando há atualizações do servidor em uma parte de relatório. Para obter mais informações, consulte a descrição de ComponentID mais à frente nessa tabela.|Sim|  
|SubType (*)|Subtipo é uma cadeia de caracteres que indica o tipo de parte de relatório para pesquisar, como "Tablix" ou "Gráfico."|Sim|  
|ComponentID (*)|ComponentID é um identificador exclusivo da parte de relatório. Esse é um novo campo adicionado ao catálogo e é visível no servidor e nos aplicativos de criação de relatório, como o Construtor de Relatórios.<br /><br /> Esse campo é usado por aplicativos cliente ao verificar atualizações de uma parte de relatório no servidor. O aplicativo cliente pesquisa o servidor em busca de ComponentIDs que estão no relatório atual do lado do cliente. Quando houver uma correspondência de ComponentID, o ModifiedDate será comparado ao SyncDate do item de relatório do lado do cliente.|N0|  
  
## Controlando o acesso a partes de relatório  
 As tabelas a seguir descrevem as atribuições de função padrão e como elas permitem executar várias operações. Os nomes de atribuição de função são diferentes dependendo do tipo de servidor de relatório que está sendo usado.  
  
### Servidor em modo nativo  
  
|Ações|Funções|  
|-------------|-----------|  
|Adicionar, excluir, editar propriedades de item, gerenciar a segurança e baixar partes de relatório|Gerenciador de Conteúdo<br /><br /> Meus Relatórios|  
|Adicionar, excluir e baixar partes de relatório|Publicador|  
|Pesquisar e reutilizar|Navegador<br /><br /> Construtor de Relatórios|  
  
### Servidor em modo integrado do SharePoint  
  
|Ações|Função|  
|-------------|----------|  
|Adicionar, excluir, editar propriedades de item, gerenciar a segurança e baixar partes de relatório|Controle total|  
|Adicionar, excluir, editar propriedades de item e baixar partes de relatório|Design<br /><br /> Contribuir|  
|Pesquisar e reutilizar|Leitura<br /><br /> Exibir Apenas|  
  
### Considerações sobre segurança  
  
-   Quando as definições de partes de relatório são reutilizadas em um relatório, elas são copiadas na definição do relatório em sua totalidade, junto com o ComponentID que as identifica. Se uma parte de relatório for atualizada no servidor, os usuários poderão escolher baixar as partes de relatório atualizadas aos seus relatórios. As atualizações também são cópias completas da parte de relatório, substituindo a versão existente da parte de relatório que estava no relatório.  
  
    > [!IMPORTANT]  
    >  Em cada uma dessas etapas, verifique se as partes de relatórios estão sendo reutilizadas em relatórios de locais e usuários confiáveis.  
  
-   As partes de relatório usam as mesmas políticas de permissão que as existentes no tipo de item "Resource". Dentro de uma pasta, não há nenhuma diferenciação entre itens de recurso tradicionais e partes de relatório a partir de uma perspectiva de herança de segurança. A parte de relatório herdará a mesma política de permissão que as imagens na mesma pasta. Quando esta distinção é necessária, a segurança de nível de item pode ser configurada para as partes de relatório desejadas. Ou você pode colocar partes de relatório que deveriam estar em pastas separadas e que têm as permissões corretas configuradas.  
  
## Consulte também  
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Solução de problemas de partes de relatório (Construtor de Relatórios e SSRS)](http://msdn.microsoft.com/pt-br/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)  
  
  