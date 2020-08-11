---
title: Notas sobre a versão do Reporting Services 2017 e posterior | Microsoft Docs
description: Saiba mais detalhes sobre as alterações no SSRS (SQL Server Reporting Services) nas versões 2017 e posteriores.
ms.date: 04/28/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maggies
author: casualoak
ms.author: rhys
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 4a97ab8d68a1b265a25eb3b97a5146a402aa9b3b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247496"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>Notas sobre a versão do SSRS (SQL Server Reporting Services) 2017 e posteriores

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

Este artigo descreve as alterações no [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) para as versões 2017 e posteriores.

Para ver as notas sobre a versão dos controles do Visualizador de Relatórios, confira [Notas sobre a versão para os controles do Visualizador de Relatórios para WebForms e WinForms do SSRS](application-integration/release-notes-ssrs-application-integration.md).

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->
## <a name="sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services

## <a name="150724337714-20191101"></a>15.0.7243.37714, 01/11/2019

Versão inicial.


## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services

## <a name="1406001572-20200406"></a>14.0.600.1572, 06/04/2020 

| Problema corrigido | Detalhes |
| :---------- | :------ |
| IU do JQuery atualizada para 1.12  | &nbsp; |
| Corrigida a diferenciação entre letras maiúsculas de minúsculas na URL  | &nbsp; |
| Corrigido o posicionamento de parâmetro quando há muitos parâmetros  | &nbsp; |
| Corrigida a FindString que não funcionava na renderização HTML5  | &nbsp; |
| Bibliotecas de clientes do Analysis Services atualizadas para resolver o preterimento de TLS 1.0/1.1 | &nbsp; |

## <a name="1406001451-20191113"></a>14.0.600.1451, 13/11/2019 

| Problema corrigido | Detalhes |
| :---------- | :------ |
| Atualizações de segurança | &nbsp; |
| Os relatórios paginados não funcionaram corretamente com parâmetros de filtro quando o instantâneo está habilitado  | &nbsp; |
| Os usuários com a função de navegador e as configurações padrão não tinham permissões para baixar arquivos do Excel  | &nbsp; |
| Falha ao atualizar para o Servidor de Relatórios do Power BI do SQL Server 2016 Reporting Services durante a atualização | &nbsp; |
| Após a atualização do SQL Server 2012 Reporting Services, as assinaturas falhavam com a mensagem "Um caractere inválido foi encontrado no cabeçalho do email: ','” | &nbsp; |
| Ferramenta de configuração: cancelar as janelas modais na seção Banco de Dados reiniciava o serviço Reporting Services | &nbsp; |
| A expressão de propriedade BorderStyle dos controles TextBox não era renderizada para o formato Excel  | &nbsp; |
| Problema de paginação que podia fazer com que alguns relatórios ficassem travados renderizando a mesma página sem chegar à última página do relatório | &nbsp; |

## <a name="1406001274-20190701"></a>14.0.600.1274, 01/07/2019

| Problema corrigido | Detalhes |
| :---------- | :------ |
| Atualizações de segurança | &nbsp; |
| Não é possível selecionar dias da semana ao criar uma agenda semanal compartilhada | &nbsp; |
| O relatório não exibe retornos de carro corretamente no formato Word | &nbsp; |
| O SCOM (System Center Operations Manager) 2019 não funciona mais com atualizações recentes do SSRS 2017 | &nbsp; |
| Ocorreu um erro ao invocar a extensão de autorização para o conjunto de dados compartilhado | &nbsp; |
| Lógica alterada no procedimento armazenado GetAllProperties no SSRS 2017 e PBIRS, que faz com que o método ReportingService2010.GetProperties do ponto de extremidade de serviço Web não consiga obter nenhum dado para o relatório vinculado | &nbsp; |
| O cabeçalho de linha de grade simples no Relatório Móvel desaparece ao clicar em um item dentro da grade | &nbsp; |
| Não é possível usar o campo de data no parâmetro de assinatura controlada por dados | &nbsp; |
| O tablix aninhado mostra fonte pequena ou fonte parcial no SSRS 2016 e posterior | &nbsp; |
| Assinaturas com erro de parâmetro DateTime após o usuário com localidade diferente editar a assinatura | &nbsp; |
| A criação de uma assinatura controlada por dados com extensão de entrega nula está falhando com "Ocorreu um erro de entrega" | &nbsp; |
| A codificação de URL está incorreta ao configurar o valor no formato Excel\Word | &nbsp; |

## <a name="1406001109-20190212"></a>14.0.600.1109, 12/02/2019

| Problema corrigido | Detalhes |
| :---------- | :------ |
| O instantâneo de cache programa alterações para a "agenda específica do relatório" depois de modificar a assinatura. | &nbsp; |
| rc:Toolbar=false não está funcionando na Express Edition. | &nbsp; |
| Determinados caracteres tailandeses são renderizados incorretamente quando relatórios paginados são exportados para PDF. | &nbsp; |
| Deadlock durante a notificação de conclusão de assinaturas controladas por dados. | &nbsp; |
| Imagens incorporadas não são exibidas em determinadas circunstâncias quando se usa o parâmetro rc:ToolBar=False. | &nbsp; |
| Não é possível criar assinaturas controladas por dados para relatórios que usam parâmetros em cascata. | &nbsp; |
| Não é possível editar assinaturas configuradas com um intervalo inválido. | &nbsp; |
| Atualizações de segurança. | &nbsp; |
| A interface do usuário vinculada a relatórios não está sendo mostrada. | &nbsp; |
| Determinados relatórios paginados com controles de tablix aninhados está com fontes incorretas. | &nbsp; |
| Espaço em branco adicionado incorretamente a determinados relatórios paginados que contêm regiões de dados tablix. | &nbsp; |
| As linhas de cabeçalhos desaparecem quando as grades de dados simples de um relatório móvel são expandidas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906, 12/09/2018

Os seguintes problemas foram corrigidos:

| Problema corrigido | Detalhes |
| :---------- | :------ |
| A autenticação personalizada não está retornando informações de cookie corretas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892, 31/08/2018

| Problema corrigido | Detalhes |
| :---------- | :------ |
| A caixa de texto dentro do retângulo faz com que o retângulo não cresça na vertical quando rc:Toolbar=False e ele tem o texto longo. | &nbsp; |
| O tamanho do texto não está se ajustando caso pageHeight seja inferior a 0,5 polegada. | &nbsp; |
| O deadlock ocorre no banco de dados do catálogo do SSRS quando ele é usado com o CRM. | &nbsp; |
| Os cabeçalhos de coluna alinhados verticalmente são exibidos incorretamente ao se rolar para baixo no relatório. | &nbsp; |
| Usuários adicionados à Função de Relatórios do System Center Operations Manager têm o acesso bloqueado no portal da Web do SSRS. | &nbsp; |
| Os caracteres tailandeses não são exportados corretamente no PDF. | &nbsp; |
| Alteração de comportamento da função de navegador. | &nbsp; |
| rc:Toolbar=false não funciona na Express Edition. | &nbsp; |
| Ausência da barra de rolagem vertical na área de prompt de parâmetro. | &nbsp; |
| Runtime do relatório de dispositivo móvel atualizado. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744, 25/04/2018

| Problema corrigido | Detalhes |
| :---------- | :------ |
| A página de assinaturas controladas por dados não mostra a opção de entrega quando ela é criada. | &nbsp; |
| A atualização do SSRS 2012 para o SSRS 2017 no RSManagement resulta na geração de uma exceção em intervalos de poucos segundos. | &nbsp; |
| Não é possível alterar os valores padrão de parâmetros de vários valores no IE11. | &nbsp; |
| As agendas ficam vazias sempre que a agenda compartilhada é executada. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689, 28/02/2018

| Problema corrigido | Detalhes |
| :---------- | :------ |
| A visibilidade do Parâmetro de Relatório em um relatório vinculado é revertida após a edição das respectivas propriedades. | &nbsp; |
| O parâmetro de URL rc:Toolbar=false não funciona na Express Edition. | &nbsp; |
| Colocar expressões na caixa de texto com a propriedade CanGrow definida como false faz com que os valores não sejam exibidos. | &nbsp; |
| Link _Saiba mais_ adicionado à chave do produto (Product Key) na instalação. | &nbsp; |
| O portal da Web com autenticação de formulários personalizados ignora os cookies sliding expiration. | &nbsp; |
| Exportar para o Word cria linhas com alturas diferentes, quando o conteúdo de uma linha está vazio. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594, 09/01/2018

Algumas atualizações de segurança foram implementadas.

### <a name="140600490-20171101"></a>14.0.600.490, 01/11/2017

Problemas resolvidos com a atualização do SKU.

## <a name="140600451-20170930"></a>14.0.600.451, 30/09/2017

Versão inicial.

## <a name="next-steps"></a>Próximas etapas

[Novidades do Reporting Services (SSRS)?](what-s-new-in-sql-server-reporting-services-ssrs.md)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
