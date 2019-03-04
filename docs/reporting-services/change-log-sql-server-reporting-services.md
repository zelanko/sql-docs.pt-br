---
title: Log de alterações do SQL Server Reporting Services (SSRS) 2017 e posteriores | Microsoft Docs
ms.date: 08/31/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: casualoak
ms.author: RhysSchmidtke
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0eec59b0d2618686f866e6b7799922d9c255b238
ms.sourcegitcommit: 009bee6f66142c48477849ee03d5177bcc3b6380
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56230903"
---
# <a name="change-log-for-sql-server-reporting-services-ssrs-2017-and-later"></a>Log de alterações do SQL Server Reporting Services (SSRS) 2017 e posteriores

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

Este artigo descreve as alterações do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

### <a name="version-1406001109-released-february-12-2019"></a>Versão 14.0.600.1109, Lançamento: 12 de fevereiro de 2019

Os seguintes problemas foram corrigidos:

 - O instantâneo de cache programa alterações para a "agenda específica do relatório" depois de modificar a assinatura.
 - rc:Toolbar=false não funciona na edição Express.
 - Determinados caracteres tailandeses renderizados incorretamente ao exportar relatórios paginados para PDF.
 - Deadlock durante a notificação de conclusão de assinaturas controladas por dados
 - Imagens incorporadas não são exibidas em determinadas circunstâncias quando se usa o parâmetro rc:ToolBar=False.
 - Não é possível criar assinaturas controladas por dados para relatórios que usam parâmetros em cascata
 - Não é possível editar assinaturas configuradas com um intervalo inválido.
 - Atualizações de segurança
 - Interface do usuário vinculada a relatórios não está em exibição.
 - Determinados relatórios paginados com controles de tablix aninhados está com fontes incorretas.
 - Espaço em branco adicionado incorretamente a determinados relatórios paginados com regiões de dados tablix.
 - Linhas de cabeçalhos desaparecem ao expandir as grades de dados simples de relatório móvel.

### <a name="version-140600906-released-september-12-2018"></a>Versão 14.0.600.906, Lançamento: 12 de setembro de 2018

Os seguintes problemas foram corrigidos:

- A autenticação personalizada não está retornando informações de cookie corretas

### <a name="version-140600892-released-august-31-2018"></a>Versão 14.0.600.892, Lançamento: 31 de agosto de 2018

Os seguintes problemas foram corrigidos:

- Caixa de texto dentro do retângulo faz com que o retângulo não cresça na vertical quando rc:Toolbar=False e ele tem o texto longo 
- O tamanho do texto não está ajustando se pageHeight for inferior a 0,5 polegada 
- Um deadlock no banco de dados do catálogo SSRS quando usado com o CRM 
- Cabeçalhos de coluna alinhados verticalmente exibidos incorretamente ao rolar para baixo no relatório 
- Usuários adicionados à Função de relatórios do SCOM terão acesso bloqueado no portal da Web do SSRS 
- Caracteres tailandês não são exportados corretamente em PDF 
- Alteração de comportamento da função de navegador 
- rc:Toolbar=false não funciona na Express Edition 
- Ausência da barra de rolagem vertical na área de prompt de parâmetro 
- Tempo de execução do relatório de dispositivo móvel atualizado 

### <a name="version-140600744-released-april-25-2018"></a>Versão 14.0.600.744, Lançamento: 25 de abril de 2018 

Os seguintes problemas foram corrigidos:

- A página de assinatura controlada por dados não mostra a opção de entrega quando ela é criada
- O upgrade do SSRS 2012 para o SSRS 2017 no RSManagement rseulta na geração de uma exceção em intervalos de poucos segundos
- Não é possível alterar os valores padrão para parâmetros de vários valores no IE11
- As agendas ficam vazias sempre que a agenda compartilhada é executada

### <a name="version-140600689-released-february-28-2018"></a>Versão 14.0.600.689, Lançamento: 28 de fevereiro de 2018

Os seguintes problemas foram corrigidos:

- A visibilidade do Parâmetro de Relatório em um relatório vinculado é revertida após a edição das respectivas propriedades
- O Parâmetro de URL rc:Toolbar=false não funciona na Express Edition
- Colocar expressões na caixa de texto com a propriedade CanGrow definida como false faz com que os valores não sejam exibidos
- Link "Saiba mais" adicionado à chave do produto (Product Key) na instalação
- O portal da Web com autenticação de formulários personalizados está ignorando os cookies de sliding expiration
- Exportar para o Word cria linhas com alturas diferentes, quando o conteúdo de uma linha está vazio

### <a name="version-140600594-released-january-9-2018"></a>Versão 14.0.600.594, Lançamento: 9 de janeiro de 2018

Atualizações de segurança

### <a name="version-140600490-released-november-1-2017"></a>Versão 14.0.600.490, Lançamento: 1º de novembro de 2017

Os seguintes problemas foram corrigidos:

- Problemas resolvidos com a atualização do SKU

### <a name="version-140600451-released-september-30-2017"></a>Versão 14.0.600.451, Lançamento: 30 de setembro de 2017 

Versão inicial

## <a name="next-steps"></a>Próximas etapas

[Novidades do Reporting Services (SSRS)](what-s-new-in-sql-server-reporting-services-ssrs.md)   

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
