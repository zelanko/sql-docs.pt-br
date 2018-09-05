---
title: Log de alterações do SQL Server Reporting Services (SSRS) 2017 e posteriores | Microsoft Docs
ms.date: 08/31/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: ''
ms.topic: conceptual
author: casualoak
ms.author: edugonz
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: a89c64e6762c2dad2ad9085b27754b3920ffb917
ms.sourcegitcommit: ca5430ff8e3f20b5571d092c81b1fb4c950ee285
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381244"
---
# <a name="change-log-for-sql-server-reporting-services-ssrs-2017-and-later"></a>Log de alterações do SQL Server Reporting Services (SSRS) 2017 e posteriores

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

Este artigo descreve as alterações do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

### <a name="version-140600892-released-august-31-2018"></a>Versão 14.0.600.892, lançada em: 31 de agosto de 2018

Esses bugs foram corrigidos:

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

### <a name="version-140600744-released-april-25-2018"></a>Versão 14.0.600.744, lançada em: 25 de abril de 2018 

Esses bugs foram corrigidos:

- A página de assinatura controlada por dados não mostra a opção de entrega quando ela é criada
- O upgrade do SSRS 2012 para o SSRS 2017 no RSManagement rseulta na geração de uma exceção em intervalos de poucos segundos
- Não é possível alterar os valores padrão para parâmetros de vários valores no IE11
- As agendas ficam vazias sempre que a agenda compartilhada é executada

### <a name="version-140600689-released-february-28-2018"></a>Versão 14.0.600.689, lançada em: 28 de fevereiro de 2018

Esses bugs foram corrigidos:

- A visibilidade do Parâmetro de Relatório em um relatório vinculado é revertida após a edição das respectivas propriedades
- O Parâmetro de URL rc:Toolbar=false não funciona na Express Edition
- Colocar expressões na caixa de texto com a propriedade CanGrow definida como false faz com que os valores não sejam exibidos
- Link "Saiba mais" adicionado à chave do produto (Product Key) na instalação
- O portal da Web com autenticação de formulários personalizados está ignorando os cookies de sliding expiration
- Exportar para o Word cria linhas com alturas diferentes, quando o conteúdo de uma linha está vazio

### <a name="version-140600594-released-january-9-2018"></a>Versão 14.0.600.594, lançada em: 9 de janeiro de 2018

Atualizações de segurança

### <a name="version-140600490-released-november-1-2017"></a>Versão 14.0.600.490, lançada em: 1º de novembro de 2017

Esse bug foi corrigido:

- Problemas resolvidos com a atualização do SKU

### <a name="version-140600451-released-september-30-2017"></a>Versão 14.0.600.451, lançada em: 30 de setembro de 2017 

Versão inicial

## <a name="next-steps"></a>Próximas etapas

[Novidades do Reporting Services (SSRS)](what-s-new-in-sql-server-reporting-services-ssrs.md)   

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
