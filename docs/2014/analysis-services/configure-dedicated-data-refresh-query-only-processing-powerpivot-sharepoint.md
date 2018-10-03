---
title: Configurar o processamento de somente consulta (PowerPivot para SharePoint) ou a atualização de dados dedicado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5e027605-1086-4941-bb01-f315df8f829b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c3b42834bc12048680c97465810832f5431441d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168176"
---
# <a name="configure-dedicated-data-refresh-or-query-only-processing-powerpivot-for-sharepoint"></a>Configurar o processamento dedicado de atualização de dados ou de somente consulta (PowerPivot para SharePoint)
  No modo integrado do SharePoint, uma instância do servidor do Analysis Services pode ser configurada para dar suporte a um tipo específico de solicitação de processamento, como processamento de atualização de dados ou de somente consulta. Por padrão, os dois tipos de solicitação de carregamento estão habilitados. Você pode desativar qualquer um dos tipos para criar um mecanismo de consulta ou servidor de atualização de dados dedicado.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
> [!NOTE]  
>  Nesta versão, não há parâmetros de configuração para limitar o uso de memória ou de CPU para trabalhos de atualização de dados ou consultas sob demanda. Uma instância do [!INCLUDE[ssGeminiSrv](../includes/ssgeminisrv-md.md)] usará todos os recursos disponíveis para executar os trabalhos de atualização de dados e consultas que está gerenciando.  
  
 Este tópico contém as seguintes seções:  
  
 [Configurar um modo de processamento](#config)  
  
 [Alterar o número de trabalhos de atualização de dados que podem ser executados em paralelo](#change)  
  
##  <a name="config"></a> Configurar um modo de processamento  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar serviços no servidor**.  
  
2.  Na parte superior da página, em Servidor, clique na seta para baixo e, em seguida, em **Alterar Servidor**.  
  
3.  Selecione o servidor do SharePoint que tem a instância de servidor do Analysis Services que você deseja configurar.  
  
4.  Clique **SQL Server Analysis Services**.  
  
5.  Em Uso da Instância de Serviço, proceda de uma das seguintes maneiras:  
  
    1.  Desmarque a caixa de seleção **habilitar carregamento de bancos de dados somente leitura** para desativar o processamento de consulta sob demanda que ocorre sempre que um usuário abre uma pasta de trabalho que contém dados PowerPivot.  
  
    2.  Desmarque a caixa de seleção **habilitar carregamento de bancos de dados para a atualização** para desativar a atualização de dados agendada.  
  
    > [!NOTE]  
    >  A desativação da atualização de dados não remove as opções de atualização de dados dos sites do SharePoint. Os usuários que possuem pastas de trabalho PowerPivot ainda podem criar agendas para atualização de dados, mas a atualização de dados não ocorrerá nesse servidor.  
  
6.  Opcionalmente, para operações de atualização de dados, você pode alterar o número de trabalhos de atualização simultâneos. O aumento do número de trabalhos simultâneos será recomendado se o servidor for configurado apenas para atualização de dados ou se houver processadores adicionais no servidor. Você poderá reduzir o número de trabalhos simultâneos se desejar liberar recursos do sistema para mais consultas sob demanda.  
  
7.  Salve as alterações. O servidor não validará suas entradas até que um evento de processamento ocorra. Se você inserir um número inválido para trabalhos simultâneos, o erro será detectado e registrado em log quando a próxima solicitação for processada.  
  
##  <a name="change"></a> Alterar o número de trabalhos de atualização de dados que podem ser executados em paralelo  
 Um trabalho de atualização de dados é uma tarefa agendada que é adicionada a uma fila de processamento mantida e monitorada por um aplicativo de serviço PowerPivot. Um trabalho consiste em informações de agenda para uma ou mais fontes de dados em uma pasta de trabalho PowerPivot. Um trabalho separado é criado para cada agenda definida. Se um proprietário de pasta de trabalho definir uma agenda para todas as fontes de dados, apenas um trabalho será criado para toda a operação de atualização de dados. Se um proprietário de pasta de trabalho criar agendas individuais para fontes de dados externas, vários trabalhos serão criados e executados para concluir uma atualização de dados completa daquela pasta de trabalho.  
  
 Você poderá aumentar o número de trabalhos de atualização de dados que podem ser executados ao mesmo tempo se o sistema tiver a capacidade para dar suporte à carga adicional.  
  
|Configuração|Valores válidos|Description|  
|-------------|------------------|-----------------|  
|Valor padrão|Calculado com base na RAM.|O valor padrão é baseado na quantidade de memória disponível dividida por 4 gigabytes. O padrão é calculado por uma fórmula de maneira que as configurações possam ser ajustadas de acordo com as funcionalidades do sistema.<br /><br /> Observação: O divisor de 4 gigabytes foi selecionado com base no uso de RAM para uma amostragem grande de fontes de dados PowerPivot reais. Não se baseia na arquitetura física ou lógica do PowerPivot.|  
|Valor máximo|Calculado com base no número de CPUs.|O número máximo de trabalhos simultâneos que podem ser especificados tem como base o número de processadores no computador. Por exemplo, em um computador quad core de 4 soquetes, o número máximo de trabalhos que podem ser executados simultaneamente é 16.|  
  
#### <a name="increasing-the-default-value-to-a-higher-value"></a>Aumentando o valor padrão para um valor mais alto  
 O gráfico a seguir mostra diferentes combinações de RAM e CPU, e os valores padrão e máximo resultantes que são calculados com base em características do sistema. Lembre-se de que o valor padrão calculado para o número de trabalhos de atualização de dados que podem ser executados simultaneamente está baseado na memória do sistema, enquanto o valor máximo calculado se baseia em CPUs. A última coluna indica se você pode aumentar o número máximo de trabalhos de atualização de dados simultâneos.  
  
|RAM real (em gigabytes)|Valor padrão calculado|Número real de CPUs|Valor máximo calculado|Aumentar trabalhos simultâneos?|  
|---------------------------------|------------------------------|------------------------|------------------------------|-------------------------------|  
|4|1|1|1|Nenhum. Os números padrão e máximo são iguais.|  
|4|1|4|4|Sim. Você pode aumentar o número de trabalhos simultâneos para 2, 3 ou 4.|  
|8|2|4|4|Sim. Você pode aumentar o número de trabalhos simultâneos para 3 ou 4.|  
|16|4|4|4|Nenhum. Os números padrão e máximo são iguais.|  
|32|Usando a fórmula que calcula o valor padrão, o padrão seria 8. Como o padrão é superior ao máximo permitido, o padrão calculado não é usado neste caso.|4|4|Nenhum. Embora a RAM grande indique um padrão de 8 trabalhos simultâneos, um computador que tenha apenas 4 processadores somente dará suporte a um máximo de 4 trabalhos simultâneos.|  
|32|8|8|8|Nenhum.|  
|32|8|16|16|Sim.|  
|64|16|16|16|Nenhum.|  
  
 Como não há como saber com antecedência se vários trabalhos podem executar com êxito ao mesmo tempo, você deve aumentar o número de trabalhos simultâneos apenas depois de analisar o consumo de memória ao longo do tempo e determinar se a memória do servidor geralmente é subutilizada.  
  
 Cada trabalho de atualização de dados terá características diferentes de carga dependendo do número e do tamanho das fontes de dados que estão sendo atualizadas. As pastas de trabalho que têm uma única fonte de dados com um número menor de linhas têm uma carga de processamento muito mais leve do que uma pasta de trabalho que tem numerosas fontes de dados e conjuntos de linhas muito grandes.  
  
## <a name="see-also"></a>Consulte também  
 [Atualização de dados PowerPivot com SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
  
