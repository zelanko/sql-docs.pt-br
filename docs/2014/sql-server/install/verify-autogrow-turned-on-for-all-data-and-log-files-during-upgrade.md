---
title: Verifique se o crescimento automático está ativado para todos os arquivos de log e de dados durante o processo de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log files [SQL Server], size
- data files [SQL Server], size
- tempdb [SQL Server], size
- autogrow [SQL Server]
ms.assetid: a5860904-e2be-4224-8a51-df18a10d3fb9
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b903e8f22fce7404f418cfc0a81ac81e954ab06f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006534"
---
# <a name="verify-autogrow-is-turned-on-for-all-data-and-log-files-during-the-upgrade-process"></a>Verificar se o crescimento automático está ativado em todos os arquivos de dados e de log durante o processo de atualização
  O Supervisor de Atualização detectou arquivos de dados ou de log que não estão com a opção de crescimento automático ativada. Recursos novos e aprimorados exigem espaço adicional em disco para bancos de dados de usuário e o **tempdb** banco de dados do sistema. Para garantir recursos acomodem esse crescimento durante as operações de atualização e produção subsequente, recomendamos definir o crescimento automático como ON para todos os arquivos de log e de dados de usuário e o **tempdb** dados e arquivos de log antes de atualizar.  
  
 Depois de atualizar e testar as cargas de trabalho, convém desativar o crescimento automático ou ajustar o incremento FILEGROWTH para os arquivos de log e de dados do usuário. É recomendável que o crescimento automático permanecem para o **tempdb** banco de dados do sistema. Para obter mais informações, consulte ‘Planejamento de capacidade para tempdb’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 **arquivos de dados**  
  
 A tabela a seguir lista as alterações em recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que resultam em requisitos de espaço em disco adicionais para arquivos de dados definidos pelo usuário.  
  
|Recurso|Alterações introduzidas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Texto completo|O mapeamento da DOCID (identificação do documento) é armazenado no arquivo de dados e não no catálogo de texto completo.|  
|Colunas `text`, `ntext` e `image`|Colunas LOB (objetos grandes) definidas como tipos de dados `text`, `ntext` ou `image` exigem 40 bytes de espaço em disco adicional por coluna. Esse aumento de espaço único ocorre durante a primeira atualização de cada coluna LOB.|  
|metadados|Metadados de sistema adicionais são criados e mantidos no grupo de arquivos PRIMARY de cada banco de dados de usuário para objetos de banco de dados e permissões de usuários. Por exemplo, em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as permissões associadas a um concessor ou ao usuário autorizado eram armazenadas em uma linha única como um bitmap. O bitmap foi expandido em várias linhas.<br /><br /> Durante o processo de atualização, deve haver espaço em disco suficiente para armazenar ambos os metadados antigos e novos. Os metadados antigos são excluídos depois que a atualização é concluída.|  
  
 **Arquivos de log de transações**  
  
 A tabela a seguir lista as alterações em recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que resultam em requisitos de espaço em disco adicionais para arquivos de log de transações definidos pelo usuário.  
  
|Recurso|Alterações introduzidas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Restauração e recuperação|Durante a fase desfazer de uma recuperação de pane, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que os usuários acessem o banco de dados. Isso é possível porque as transações não confirmadas no momento da falha readquirem todos os bloqueios que tinham antes da falha. Enquanto essas transações estão sendo revertidas, seus bloqueios as protegem de interferências dos usuários. Essas informações de bloqueio adicionais devem ser mantidas no log de transações.|  
  
 **arquivos de log e de dados tempdb**  
  
 Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o **tempdb** banco de dados é usado para armazenar os seguintes objetos:  
  
-   Objetos temporários criados explicitamente como tabelas, procedimentos armazenados, variáveis de tabela ou cursores.  
  
-   Tabelas de trabalho internas criadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Resulta das classificações temporárias quando você cria ou recria índices, se SORT_IN_TEMPDB for especificado.  
  
 Objetos adicionais também usam o **tempdb** banco de dados. A tabela a seguir lista as alterações ou adições ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos que resultam em mais espaço em disco para **tempdb** dados e arquivos de log.  
  
|Recurso|Alterações introduzidas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Controle de versão de linha|O controle de versão de linha é uma estrutura geral do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada para:<br /><br /> Oferece suporte a gatilhos: criar as tabelas inseridas e excluídas em gatilhos. Qualquer linha modificada pelo gatilho tem controle de versão. Isso inclui as linhas modificadas pela instrução que iniciou o gatilho, bem como quaisquer modificações de dados feitas pelo gatilho. Gatilhos AFTER usam o repositório de versão **tempdb** para manter as imagens anteriores das linhas alteradas pelo gatilho. Quando você carrega dados em massa com gatilhos habilitados, uma cópia de cada linha é adicionada ao repositório da versão.<br /><br /> Oferecer suporte a vários conjuntos de resultados ativos (MARS) Se uma sessão MARS emitir uma instrução de modificação de dados (como INSERT, UPDATE ou DELETE) cada vez que houver um conjunto de resultados ativos, as linhas afetadas pela instrução de modificação terão controle de versão.<br /><br /> Oferecer suporte a operações de índice que especificam a opção ONLINE. As operações de índice online utilizam o controle de versão de linha para isolar a operação de índice dos efeitos das modificações feitas por outras transações. Isso evita a necessidade de solicitar bloqueios de compartilhamento de linhas já lidas. Além disso, o usuários simultâneos atualizar e excluir operações durante o índice online operações exigem espaço para registros de versão no **tempdb**.<br /><br /> Suporte a níveis de isolamento de transação com base em controle de versão de linha: uma nova implementação de leitura confirmada nível de isolamento que usa o controle de versão de linha para fornecer consistência de leitura em nível de instrução. Um novo nível de isolamento, instantâneo, para fornecer a consistência de leitura em nível de transações.<br /><br /> <br /><br /> Versões de linha são mantidas no **tempdb** longo o suficiente para atender os requisitos das transações executadas em níveis de isolamento com base em controle de versão de linha de armazenamento de versão.<br /><br /> Para obter mais informações sobre controle de versão de linha e repositório de versão, consulte o tópico ‘Compreendendo níveis de isolamento com base em controle de versão de linha’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Armazenando metadados de tabela e variáveis temporárias em cache|Para todos os metadados de tabela temporária e variável temporária armazenados no cache de metadados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], duas páginas extras são alocadas para **tempdb**.<br /><br /> Se um procedimento armazenado ou gatilho criar uma tabela temporária ou variável temporária, o objeto temporário não será excluído quando o procedimento ou gatilho concluir a execução. Em vez disso, o objeto temporário fica truncado em uma página e é usado novamente a próxima vez que o procedimento ou gatilho é executado.|  
|Índices em tabelas particionadas|Quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] faz uma classificação para criar índices particionados, espaço suficiente para manter a execução intermediária de classificação de cada partição é necessário em **tempdb** se a opção de índice SORT_IN_TEMPDB for especificada.|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|[!INCLUDE[ssSB](../../includes/sssb-md.md)] usa explicitamente **tempdb** ao preservar o contexto de caixa de diálogo existente que não pode ficar na memória (aproximadamente 1 KB por caixa de diálogo).<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa implicitamente **tempdb** pelo cache de objetos no contexto de execução da consulta. Por exemplo, tabelas de trabalho usadas para eventos de timer e plano de fundo entregaram conversações.<br /><br /> Os recursos DBMail, notificações de eventos e notificações de consulta usam o [!INCLUDE[ssSB](../../includes/sssb-md.md)] implicitamente.|  
|Tipos de dados LOB (objeto grande)<br /><br /> Variáveis e parâmetros LOB|Os tipos de dados `varchar(max)`, `nvarchar(max)`, **texto varbinary (max)**, `ntext`, `image,` e `xml` são tipos de objeto grande.<br /><br /> Quando um nível de isolamento da transação com base em controle de versão de linha é habilitado no banco de dados e são feitas modificações de objetos grandes, o fragmento alterado LOB é copiado no repositório de versão no **tempdb**.<br /><br /> Parâmetros definidos como um tipo de dados de objeto grande são armazenados em **tempdb**.|  
|CETs (expressões de tabela comuns)|Tabelas de trabalho temporárias para operações de spool são criadas no **tempdb** quando são executadas consultas de expressão de tabela comuns.|  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para definir um arquivo de log ou de dados para crescimento automático, modifique as seguintes instruções para especificar os dados e o log para seu banco de dados. Você deve ajustar o incremento FILEGROWTH para um valor que é apropriado para seu ambiente.  
  
```  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = tempdev,  
    FILEGROWTH = 20MB);  
GO  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = templog,  
    FILEGROWTH = 10MB);  
```  
  
 O incremento de crescimento padrão para arquivos de dados é 1 MB. O arquivo de log padrão é 10%. Nós recomendamos as seguintes políticas gerais para definir o incremento FILEGROWTH:  
  
|Tamanho de arquivo|Incremento FILEGROWTH|  
|---------------|--------------------------|  
|0 a 50 MB|10MB|  
|100 a 200 MB|20MB|  
|500 MB ou mais|10%|  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
