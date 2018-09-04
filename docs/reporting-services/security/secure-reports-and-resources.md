---
title: Proteger relatórios e recursos | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], reports
- security [Reporting Services], resources
- reports [Reporting Services], security
- confidential reports [Reporting Services]
- resources [Reporting Services], security
ms.assetid: 63cd55c7-fd2a-49e3-a3f8-59eb1a1c6e83
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5320c2a40106c8bbdaa2417fc2a74f19e2c76d6a
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43266328"
---
# <a name="secure-reports-and-resources"></a>Proteger relatórios e recursos
  É possível definir a segurança de relatórios e recursos individuais para controlar o nível de acesso que os usuários têm a esses itens. Por padrão, somente os usuários que são membros do grupo interno de **Administradores** podem executar relatórios, exibir recursos, modificar propriedades e excluir os itens. Todos os outros usuários devem ter atribuições de função que permitam o acesso a um relatório ou recurso.  
  
## <a name="role-based-access-to-reports-and-resources"></a>Access baseado em funções a relatórios e recursos  
 Para conceder acesso a relatórios e recursos, você pode permitir que os usuários herdem as atribuições de função existentes de uma pasta pai ou criem uma nova atribuição de função no próprio item.  
  
 Na maioria dos casos, você provavelmente vai usar as permissões que são herdadas de uma pasta pai. A definição de segurança em relatórios e recursos individuais é necessária somente se você desejar ocultar o relatório ou recurso dos usuários que não precisam saber de sua existência ou desejar aumentar o nível de acesso para um relatório ou item. Esses objetivos não são mutuamente exclusivos. Você pode restringir o acesso a um relatório a um grupo menor de usuários e fornecer a todos ou a alguns deles privilégios adicionais para gerenciar o relatório.  
  
 Você talvez precise criar várias atribuições de função para alcançar seus objetivos. Por exemplo, suponha que você queira disponibilizar um relatório para dois usuários Ann e Fernando, e para o grupo Gerentes de Recursos Humanos. Ann e Fernando devem poder gerenciar o relatório, mas os membros do grupo só precisam executá-lo. Para acomodar todos esses usuários, você deveria criar três atribuição de função separadas: uma para que Ann fosse gerente de conteúdo do relatório, uma para Fernando ser gerente de conteúdo do relatório e outra para dar suporte a tarefas de somente exibição para o grupo Gerentes de Recursos Humanos.  
  
 Depois de definir a segurança em um relatório ou recurso, essas configurações permanecem com o item, mesmo que ele seja movido para um novo local. Por exemplo, se você mover um relatório ao qual somente poucas pessoas têm acesso, o relatório continuará disponível somente para esses usuários mesmo que seja movido para uma pasta que tem uma política de segurança relativamente aberta.  
  
## <a name="mitigating-html-injection-attacks-in-a-published-report-or-document"></a>Diminuindo ataques de injeção HTML em um relatório ou documento publicado  
 No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], relatórios e recursos são processados com a identidade de segurança do usuário que está executando o relatório. Se o relatório contiver expressões, scripts, itens de relatório personalizados ou assemblies personalizados, o código será executado com as credenciais do usuário. Se um recurso for um documento HTML que contém script. o script será executado quando o usuário abrir o documento no servidor de relatório. A possibilidade de executar scripts ou códigos em um relatório é um recurso avançado que pode ser um pouco arriscado. Se o código for suspeito, o servidor de relatório e o usuário que está executando o relatório estarão vulneráveis a ataques.  
  
 Ao conceder acesso a relatórios e recursos processados como HTML, é importante lembrar que os relatórios são processados em confiança total e que scripts possivelmente suspeitos podem ser enviados ao cliente. Dependendo das configurações do navegador, o cliente executará o HTML no nível de confiança especificado no navegador.  
  
 Você pode diminuir o risco de executar scripts suspeitos tomando as seguintes precauções:  
  
-   Tome cuidado ao decidir quem pode publicar conteúdo em um servidor de relatório. Como conteúdos suspeitos podem ser publicados, limite os usuários que podem publicar conteúdo a um pequeno número de usuários confiáveis.  
  
-   Todos os editores devem evitar publicar relatórios e recursos provenientes de origens desconhecidas ou não confiáveis. Se necessário, abra o arquivo em um editor de textos e procure scripts e URLs suspeitos.  
  
## <a name="report-parameters-and-script-injection"></a>Parâmetros de Relatórios e Injeção de Script  
 Os Parâmetros de Relatório proporcionam flexibilidade para o projeto geral e a emissão do relatório. Porém, essa mesma flexibilidade pode, em alguns casos, ser usada por um invasor em ataques de atração. Para atenuar o risco de execução acidental de scripts mal-intencionados, abra apenas relatórios renderizados de fontes confiáveis. Recomenda-se que você considere o seguinte cenário, que é um potencial ataque de injeção de script ao Renderizador de HTML:  
  
1.  Um relatório contém uma caixa de texto com a ação de hiperlink definida como o valor de um parâmetro que pode conter texto mal-intencionado.  
  
2.  O relatório é publicado em um servidor de relatórios ou de outra forma disponibilizado de modo que o valor de parâmetro de relatório possa ser controlado pela URL de uma página da Web.  
  
3.  Um invasor cria um link para a página da Web ou o servidor de relatório, especificando o valor do parâmetro no formato “javascript:\<malicious script here>” e envia esse link a outra pessoa em um ataque de atração.  
  
## <a name="mitigating-script-injection-attacks-in-a-hyperlink-in-a-published-report-or-document"></a>Atenuando ataques de injeção de script em um hiperlink de um relatório ou documento publicado  
 Relatórios podem conter hiperlinks inseridos no valor da propriedade Action de um item de relatório ou parte de um item de relatório. Hiperlinks podem ser associados a dados que recuperados de uma fonte de dados externa quando o relatório é processado. Se um usuário mal-intencionado modificar os dados subjacentes, o hiperlink pode correr o risco de explorações de script. Se um usuário clicar no link no relatório publicado ou exportado, o script mal-intencionado pode ser executado.  
  
 Para atenuar o risco de incluir links em um relatório que executam inadvertidamente scripts mal-intencionados, associe hiperlinks a dados apenas de fontes confiáveis. Verifique se os dados dos resultados da consulta e as expressões que associam dados a hiperlinks não criam links que possam ser explorados. Por exemplo, não baseie um hiperlink em uma expressão que concatene dados de vários campos de conjuntos de dados. Se necessário, navegue até o relatório e use "Exibir origem" para verificar scripts e URLs suspeitos.  
  
## <a name="mitigating-sql-injection-attacks-in-a-parameterized-report"></a>Diminuindo ataques de injeção SQL em um relatório parametrizado  
 Em qualquer relatório que inclua um parâmetro do tipo **String**, use uma lista de valores disponíveis (também conhecida como uma lista de valores válidos) e verifique se todos os usuários que executam o relatório têm somente as permissões necessárias para exibir os dados do relatório. Quando você define um parâmetro do tipo **String**, é exibida para o usuário uma caixa de texto que pode ter qualquer valor. Uma lista de valores disponíveis limita os valores que podem ser inseridos. Se o parâmetro do relatório estiver associado a um parâmetro de consulta e uma lista de valores disponíveis não for usada, um usuário do relatório poderá digitar sintaxe SQL na caixa de texto, abrindo potencialmente o relatório e o servidor a um ataque de injeção SQL. Se o usuário tiver permissões suficientes para executar a nova instrução SQL, resultados indesejados podem ser produzidos no servidor.  
  
 Se um parâmetro de relatório não estiver associado a um parâmetro de consulta e os valores de parâmetro forem incluídos no relatório, um usuário do relatório poderá digitar a sintaxe de expressão ou uma URL no valor de parâmetro e processar o relatório em Excel ou HTML. Se outro usuário exibir o relatório e clicar no conteúdo do parâmetro renderizado, o usuário poderá executar acidentalmente o script ou link mal-intencionado.  
  
 Para reduzir o risco de execução acidental de scripts mal-intencionados, só abra relatórios renderizados de fontes confiáveis.  
  
> [!NOTE]  
>  Em versões anteriores da documentação, foi incluído um exemplo de criação de uma consulta dinâmica como uma expressão. Esse tipo de consulta cria uma vulnerabilidade a ataques de injeção SQL e, portanto, não é recomendado.  
  
## <a name="securing-confidential-reports"></a>Protegendo relatórios confidenciais  
 Os relatórios que contêm informações confidenciais devem ser protegidos no nível de acesso aos dados, solicitando que os usuários forneçam credenciais para acessar dados confidenciais. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Você também pode proteger uma pasta deixá-la inacessível para usuários não autorizados. Para obter mais informações, consulte [Proteger pastas](../../reporting-services/security/secure-folders.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Proteger itens de fontes de dados compartilhadas](../../reporting-services/security/secure-shared-data-source-items.md)   
 [Armazenar credenciais em uma fonte de dados do Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
