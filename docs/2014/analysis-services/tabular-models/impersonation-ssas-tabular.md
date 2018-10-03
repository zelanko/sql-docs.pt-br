---
title: Representação (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6455a83328f973004f6c0e7ff39f574413693d94
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111941"
---
# <a name="impersonation-ssas-tabular"></a>Representação (SSAS tabular)
  Este tópico fornece a autores de modelos tabulares uma compreensão de como as credenciais de logon são usados pelo Analysis Services ao conectar-se a uma fonte de dados para importar e processar (atualizar) dados.  
  
 Este artigo inclui as seções a seguir:  
  
-   [Benefícios](#bkmk_how_imper)  
  
-   [Opções](#bkmk_imp_info_options)  
  
-   [Segurança](#bkmk_impers_sec)  
  
-   [Representação ao importar um modelo](#bkmk_imp_newmodel)  
  
-   [Configurando a representação](#bkmk_conf_imp_info)  
  
##  <a name="bkmk_how_imper"></a> Benefícios  
 *Representação* é a capacidade de um aplicativo de servidor, como o Analysis Services, de assumir a identidade de um aplicativo cliente. O Analysis Services é executado com uma conta de serviço, no entanto, quando o servidor estabelece uma conexão com uma fonte de dados, ele usa representação de forma que verificações de acesso para a importação e processamento de dados possam ser executadas.  
  
 As credenciais usadas para representação são diferentes das credenciais do usuário que está conectado no momento. As credenciais do usuário conectado são usadas para operações no cliente ao criar um modelo.  
  
 É importante compreender como as credenciais de representação são especificadas e protegidas e também a diferença entre contextos nos quais as credenciais do usuário conectado no momento e outras credenciais são usadas.  
  
 **Compreendendo as credenciais do lado do servidor**  
  
 No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], as credenciais são especificadas para cada fonte de dados por meio da página **Informações sobre Representação** no Assistente de Importação de Tabela ou por meio da edição de uma conexão de fonte de dados existente na caixa de diálogo **Conexões Existentes** .  
  
 Quando os dados são importados ou processados, as credenciais especificadas na página **Informações sobre Representação** são usadas para conectar-se à fonte de dados e buscar os dados. Essa é uma operação do *servidor* que é executado no contexto de um aplicativo cliente porque o servidor do Analysis Services que hospeda o banco de dados de espaço de trabalho conecta-se à fonte de dados e busca os dados.  
  
 Ao implantar um modelo no servidor do Analysis Services, se o banco de dados de espaço de trabalho estiver na memória quando o modelo for implantado, as credenciais serão passadas para o servidor do Analysis Services para o qual o modelo é implantado. Em nenhum momento as credenciais de usuário armazenados em disco.  
  
 Quando um modelo implantado processa dados de uma fonte de dados, as credenciais de representação, persistidas no banco de dados na memória, são usadas para a conexão à fonte de dados e a busca de dados. Como esse processo é tratado pelo servidor do Analysis Services que gerencia o banco de dados modelo, essa é mais uma vez uma operação do servidor.  
  
 **Compreendendo as credenciais do cliente**  
  
 Ao criar um novo modelo ou ao adicionar uma fonte de dados a um modelo existente, você usa o Assistente de Importação de Tabela para conectar-se a uma fonte de dados e selecionar tabelas e exibições a serem importadas no modelo. No Assistente de Importação de Tabela, na página **Selecionar Tabelas e Exibições** , é possível usar o recurso **Visualizar e Filtrar** para exibir um exemplo (limitado a 50 linhas) dos dados que serão importados. Você também pode especificar filtros para excluir dados que não precisam ser incluídos no modelo.  
  
 De maneira semelhante, para modelos existentes que já foram criados, você pode usar a caixa de diálogo **Editar Propriedades da Tabela** para visualizar e filtrar dados importados em uma tabela. Para visualizar e filtrar recursos aqui, use a mesma funcionalidade do recurso **Visualizar e Filtrar** na página **Selecionar Tabelas e Exibições** do Assistente de Importação de Tabela.  
  
 O recurso **Visualizar e Filtrar** e as caixas de diálogo **Propriedades da Tabela** e **Gerenciador de Partições** são uma operação do *cliente* ; isto é, o que é feito durante essa operação é diferente de como a fonte de dados é conectada e os dados são buscados da fonte de dados; uma operação do servidor. As credenciais usadas para visualizar e filtrar dados são as credenciais do usuário que está conectado no momento. As operações do cliente sempre usam as credenciais do Windows do usuário atual para conectar-se à fonte de dados.  
  
 Essa separação de credenciais usadas durante operações do servidor e do cliente pode levar a uma incompatibilidade no que o usuário vê ao usar o recurso **Visualizar e Filtrar** ou a caixa de diálogo **Propriedades da Tabela** (operações do cliente) e os dados que serão buscados durante uma importação ou processamento (uma operações do servidor). Se as credenciais do usuário conectado no momento e as credenciais de representação especificadas forem diferentes, os dados vistos no recurso **Visualizar e Filtrar** ou na caixa de diálogo **Propriedades da Tabela** e os dados buscados durante uma importação ou processamento poderão ser diferentes dependendo das credenciais requeridas pela fonte de dados.  
  
> [!IMPORTANT]  
>  Ao criar um modelo, verifique se as credenciais do usuário conectado no momento e as credenciais especificadas para representação têm direitos suficientes para buscar os dados da fonte de dados.  
  
##  <a name="bkmk_imp_info_options"></a> Opções  
 Ao configurar a representação, ou ao editar propriedades para uma conexão à fonte de dados existente no Analysis Services, você pode especificar um das opções a seguir:  
  
|Opção|ImpersonationMode<sup>1</sup>|Description|  
|------------|-----------------------------------|-----------------|  
|**Nome de usuário específicos do Windows e senha** <sup>2</sup>|ImpersonateWindowsUserAccount|Esta opção especifica que o modelo usa uma conta de usuário do Windows para importar ou processar dados da fonte de dados. O domínio e o nome da conta de usuário usa o seguinte formato:**\<nome de domínio >\\< nome da conta de usuário\>**. Ao criar um novo modelo por meio do Assistente de Importação de Tabela, essa é a opção padrão.|  
|**Conta de Serviço**|ImpersonateServiceAccount|Esta opção especifica que o modelo usa as credenciais de segurança associadas à instância de serviço do Analysis Services que gerencia o modelo.|  
  
 <sup>1</sup>ImpersonationMode Especifica o valor para o [elemento DataSourceImpersonationInfo &#40;ASSL&#41; ](../scripting/properties/impersonationinfo-element-assl.md) propriedade na fonte de dados.  
  
 <sup>2</sup>ao usar essa opção, se o banco de dados do espaço de trabalho for removido da memória, devido a uma reinicialização ou o **retenção de espaço de trabalho** estiver definida como **descarregar da memória** ou  **Excluir do espaço de trabalho**, e o projeto de modelo é fechado, na sessão subsequente, se você tentar processar dados de tabela, você será solicitado a inserir as credenciais para cada fonte de dados. De maneira semelhante, se um banco de dados modelo implantado for removido da memória, as credenciais para cada fonte de dados serão solicitadas a você.  
  
##  <a name="bkmk_impers_sec"></a> Segurança  
 As credenciais usadas com representação são persistidas na memória pelo mecanismo analítico na memória xVelocity (VertiPaq) associado ao servidor do Analysis Services que gerencia o banco de dados de espaço de trabalho ou um modelo implantado.  Em nenhum momento as credenciais são gravadas em disco. Se o banco de dados de espaço de trabalho não estiver na memória quando o modelo for implantado, o usuário será solicitado a digitar as credenciais usadas para conectar-se à fonte de dados e buscar dados.  
  
> [!NOTE]  
>  É recomendável especificar uma conta de usuário do Windows e uma senha para credenciais de representação. Uma conta de usuário do Windows pode ser configurada para usar privilégios mínimos necessários conectar-se e ler dados da fonte de dados.  
  
##  <a name="bkmk_imp_newmodel"></a> Representação ao importar um modelo  
 Ao contrários dos modelos tabulares, que podem usar vários diferentes modos de representação para dar suporte à coleta de dados fora do processo, o PowerPivot usa apenas um modo, o ImpersonateCurrentUser. Como o PowerPivot sempre é executado em processo, ele conecta-se a fontes de dados por meio das credenciais do usuário conectado no momento. Em modelos tabulares, as credenciais do usuário conectado no momento são usadas apenas com o recurso **Visualizar e Filtrar** no Assistente de Importação de Tabela e ao exibir as **Propriedades da Tabela**. As credenciais de representação usadas ao importar ou processar dados no banco de dados de espaço de trabalho ou ao importar ou processar dados em um modelo implantado.  
  
 Ao criar um novo modelo com a importação de uma pasta de trabalho PowerPivot existente, por padrão, o designer de modelo configurará a representação para usar a conta de serviço (ImpersonateServiceAccount). É recomendável alterar as credenciais de representação em modelos importados PowerPivot para uma conta de usuário do Windows. Depois que a pasta de trabalho do PowerPivot foi importada e o novo modelo criado no designer de modelo, você pode alterar as credenciais usando o **conexões existentes** caixa de diálogo.  
  
 Ao criar um novo modelo com a importação de um modelo existente em um servidor do Analysis Services, as credenciais de representação são passadas do banco de dados modelo existente para o novo banco de dados de espaço de trabalho modelo. Se necessário, você pode alterar as credenciais no novo modelo com o uso da caixa de diálogo **Conexões Existentes** .  
  
##  <a name="bkmk_conf_imp_info"></a> Configurando a representação  
 O local e o contexto onde um modelo existe determinará como as informações de representação serão configuradas. Para modelos que estão sendo criados no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode configurar informações de representação na página **Informações sobre Representação** no Assistente de Importação de Tabela ou por meio da edição de uma conexão de fonte de dados na caixa de diálogo **Conexões Existentes** . Para exibir conexões existentes, no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no menu **Model** , clique em **Conexões Existentes**.  
  
 Para modelos que são implantados em um servidor do Analysis Services, informações de representação podem ser configuradas clicando no botão de reticências (...) do **informações de representação de fonte de dados** propriedade no **depropriedadesdebancodedados** caixa de diálogo de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](directquery-mode-ssas-tabular.md)   
 [Fontes de dados &#40;Tabular do SSAS&#41;](../data-sources-ssas-tabular.md)   
 [Implantação de solução de modelo de tabela &#40;Tabular do SSAS&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
