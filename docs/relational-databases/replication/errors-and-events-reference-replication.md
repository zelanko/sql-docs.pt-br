---
title: "Referência de erros e eventos (replicação) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], errors
- replication [SQL Server], troubleshooting
- errors [SQL Server replication]
- errors and events reference [SQL Server replication]
ms.assetid: e67d1bab-47b6-441d-ab9c-251a2ca499e1
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 29667a31a69460d6408a84d21035a1a16cf4dc31
ms.lasthandoff: 04/11/2017

---
# <a name="errors-and-events-reference-replication"></a>Referência de erros e eventos (replicação)
  Esta seção da documentação contém informações sobre causa e resolução de diversos erros relacionados à replicação.  
  
|Erro|Mensagem|  
|-----------|-------------|  
|[MSSQL_ENG002601](../../relational-databases/replication/mssql-eng002601.md)|Não é possível inserir uma linha de chave duplicada no objeto '%.*ls' com o índice exclusivo '%.\*ls'.|  
|[MSSQL_ENG002627](../../relational-databases/replication/mssql-eng002627.md)|Violação da restrição %ls '%.*ls'. Não é possível inserir uma chave duplicada no objeto '%.\*ls'.|  
|[MSSQL_ENG003165](../../relational-databases/replication/mssql-eng003165.md)|O banco de dados '% ls' foi restaurado, mas houve um erro durante a restauração/remoção da replicação. O banco de dados foi deixado offline. Consulte o tópico MSSQL_ENG003165 dos Manuais Online do SQL Server.|  
|[MSSQL_ENG003724](../../relational-databases/replication/mssql-eng003724.md)|Não é possível %S_MSG o %S_MSG '%.*ls' porque está sendo usado para replicação.|  
|[MSSQL_ENG004929](../../relational-databases/replication/mssql-eng004929.md)|Não é possível alterar %S_MSG '%.*ls' porque ele está sendo publicado para replicação.|  
|MSSQL_ENG007395. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Não é possível iniciar uma transação aninhada para o provedor de OLE DB "% ls" para o servidor vinculado "% ls." Uma transação aninhada era necessária porque a opção XACT_ABORT estava definida como OFF."|  
|[MSSQL_ENG014005](../../relational-databases/replication/mssql-eng014005.md)|Não foi possível descartar a publicação. Existe uma assinatura para ela.|  
|[MSSQL_ENG014010](../../relational-databases/replication/mssql-eng014010.md)|O servidor '%s' não está definido como um servidor de assinatura.|  
|[MSSQL_ENG014114](../../relational-databases/replication/mssql-eng014114.md)|'%s' não está configurado como um Distributor.|  
|[MSSQL_ENG014117](../../relational-databases/replication/mssql-eng014117.md)|'%s' não está configurado como um banco de dados de distribuição.|  
|[MSSQL_ENG014120](../../relational-databases/replication/mssql-eng014120.md)|Não foi possível descartar o banco de dados de distribuição '%s'. O banco de dados do distribuidor está associado a um Publicador.|  
|[MSSQL_ENG014121](../../relational-databases/replication/mssql-eng014121.md)|Não foi possível descartar o Distribuidor '%s'. Esse Distribuidor possui bancos de dados de distribuição associados.|  
|[MSSQL_ENG014144](../../relational-databases/replication/mssql-eng014144.md)|Não é possível descartar o Assinante '%s'. Existem assinaturas para ele no banco de dados de publicação '%s'.|  
|[MSSQL_ENG014150](../../relational-databases/replication/mssql-eng014150.md)|Replicação-%s: agente %s bem-sucedida. %s|  
|[MSSQL_ENG014151](../../relational-databases/replication/mssql-eng014151.md)|Replicação-%s: falha no agente %s. %s|  
|[MSSQL_ENG014152](../../relational-databases/replication/mssql-eng014152.md)|Replicação-%s: agente %s agendado para tentar novamente. %s|  
|[MSSQL_ENG014157](../../relational-databases/replication/mssql-eng014157.md)|A assinatura criada pelo Assinante '%s' para a publicação '%s' expirou e foi descartada.|  
|[MSSQL_ENG014160](../../relational-databases/replication/mssql-eng014160.md)|O limite [%s:%s] da publicação [%s] foi definido. Uma ou mais assinaturas nesta publicação expiraram.|  
|[MSSQL_ENG014161](../../relational-databases/replication/mssql-eng014161.md)|O limite [%s:%s] da publicação [%s] foi definido. Verifique se o leitor de log e os agentes de distribuição estão em execução e atendem ao requisito de latência.|  
|[MSSQL_ENG014162](../../relational-databases/replication/mssql-eng014162.md)|O limite [%s:%s] da publicação [%s] foi definido. Verifique se o agente de mesclagem está sendo executado e pode atender ao requisito esperado.|  
|[MSSQL_ENG014163](../../relational-databases/replication/mssql-eng014163.md)|O limite [%s:%s] da publicação [%s] foi definido. Verifique se o agente de mesclagem está sendo executado e pode atender ao requisito esperado.|  
|[MSSQL_ENG014164](../../relational-databases/replication/mssql-eng014164.md)|O limite [%s:%s] da publicação [%s] foi definido. Verifique se o agente de mesclagem está sendo executado e pode atender ao requisito esperado.|  
|[MSSQL_ENG014165](../../relational-databases/replication/mssql-eng014165.md)|O limite [%s:%s] da publicação [%s] foi definido. Verifique se o agente de mesclagem está sendo executado e pode atender ao requisito esperado.|  
|[MSSQL_ENG018456](../../relational-databases/replication/mssql-eng018456.md)|Falha no logon do usuário '%.*ls'.%.\*ls|  
|[MSSQL_ENG018752](../../relational-databases/replication/mssql-eng018752.md)|Somente um Agente de Leitor de Log ou um procedimento relacionado ao log (sp_repldone, sp_replcmds e sp_replshowcmds) pode se conectar ao banco de dados de cada vez. Se você tiver executado um procedimento relacionado ao log, descarte a conexão através da qual o procedimento foi executado ou execute sp_replflush por essa conexão antes de iniciar o Agente de Leitor de Log ou de executar outro procedimento relacionado ao log.|  
|[MSSQL_ENG020554](../../relational-databases/replication/mssql-eng020554.md)|O agente de replicação não registrou uma mensagem de progresso em %ld minutos. Isso pode indicar inoperância do agente ou alta atividade do sistema. Verifique se os registros estão sendo replicados no destino e se as conexões com o Assinante, o Publicador e o Distribuidor ainda estão ativas.|  
|[MSSQL_ENG020557](../../relational-databases/replication/mssql-eng020557.md)|Desligamento do agente. Para obter mais informações, consulte o histórico de trabalho do SQL Server Agent relacionado ao trabalho '%s'.|  
|[MSSQL_ENG020572](../../relational-databases/replication/mssql-eng020572.md)|A assinatura do assinante '%s' para o artigo '%s' na publicação '%s' foi reiniciada após uma falha na validação.|  
|[MSSQL_ENG020574](../../relational-databases/replication/mssql-eng020574.md)|Falha na validação de dados na assinatura do assinante '%s' para o artigo '%s' na publicação '%s'.|  
|[MSSQL_ENG020575](../../relational-databases/replication/mssql-eng020575.md)|Êxito na validação de dados da assinatura do assinante '%s' para o artigo '%s' na publicação '%s'.|  
|[MSSQL_ENG020596](../../relational-databases/replication/mssql-eng020596.md)|Somente '%s' ou membros de db_owner podem descartar o agente anônimo.|  
|[MSSQL_ENG020598](../../relational-databases/replication/mssql-eng020598.md)|A linha não foi encontrada no Assinante ao aplicar o comando replicado.|  
|[MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md)|O instantâneo inicial da publicação '%s' ainda não está disponível.|  
|[MSSQL_ENG021076](../../relational-databases/replication/mssql-eng021076.md)|O instantâneo inicial do artigo '%s' ainda não está disponível.|  
|[MSSQL_ENG021286](../../relational-databases/replication/mssql-eng021286.md)|A tabela de conflitos '%s' não existe.|  
|[MSSQL_ENG021330](../../relational-databases/replication/mssql-eng021330.md)|Falha ao criar um subdiretório no diretório de trabalho da replicação.(% ls)|  
|[MSSQL_ENG021331](../../relational-databases/replication/mssql-eng021331.md)|Falha ao copiar o arquivo de script de usuário para o Distribuidor.(% ls)|  
|[MSSQL_ENG021385](../../relational-databases/replication/mssql-eng021385.md)|Falha no instantâneo ao processar a publicação '%s'. Possivelmente devido à atividade de alteração de esquema ativa ou à adição de novos artigos.|  
|MSSQL_ENG021617. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Não é possível executar o SQL*PLUS. Certifique-se de que há uma versão atual do código de cliente Oracle instalada no distribuidor.|  
|MSSQL_ENG021620. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|A versão do SQL*PLUS acessível através da variável de sistema Path não está atualizada o bastante para oferecer suporte à edição Oracle. Certifique-se de que há uma versão atual do código de cliente Oracle instalada no distribuidor.|  
|MSSQL_ENG021624. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Não é possível localizar o provedor OLE DB Oracle registrado, OraOLEDB.Oracle, no distribuidor '%s.' Certifique-se de que uma versão atual do provedor OLE DB Oracle foi instalada e registrada no distribuidor.|  
|MSSQL_ENG021626. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Não é possível fazer conexão com o servidor de banco de dados Oracle '%s' usando o provedor OLE DB Oracle OraOLEDB.Oracle.|  
|MSSQL_ENG021627. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Não é possível fazer conexão com o servidor de banco de dados Oracle '%s' usando o provedor OLE DB Microsoft MSDAORA.|  
|MSSQL_ENG021628. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Não é possível atualizar o Registro do distribuidor '%s' para permitir que o provedor OLE DB Oracle OraOLEDB.Oracle seja executado em processo com o SQL Server. Certifique-se de que o logon atual tem autorização para modificar as chaves do Registro que pertencem ao SQL Server.|  
|MSSQL_ENG021629. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|A chave do Registro CLSID indicando que o provedor OLE DB Oracle para Oracle, OraOLEDB.Oracle, foi registrado não está presente no distribuidor. Certifique-se de que o provedor OLE DB Oracle esteja instalado e registrado no distribuidor.|  
|MSSQL_ENG021642. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Publicadores heterogêneos requerem um servidor vinculado. Já existe um servidor vinculado nomeado '%s'. Remova o servidor vinculado ou escolha um nome de publicador diferente.|  
|MSSQL_ENG021663. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Não foi encontrada nenhuma chave primária válida para a tabela de origem [% s].[% s].|  
|MSSQL_ENG021684. Consulte [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|As permissões associadas com o logon de administrador para o publicador Oracle '% s' não é suficiente.|  
|[MSSQL_ENG021797](../../relational-databases/replication/mssql-eng021797.md)|'%s' deve ser um logon válido do Windows na forma: 'MACHINE\Login' ou 'DOMAIN\Login'. Consulte a documentação de '%s'.|  
|[MSSQL_ENG021798](../../relational-databases/replication/mssql-eng021798.md)|O trabalho do agente '%s' deve ser adicionado via '%s' antes de continuar. Consulte a documentação de '%s'.|  
|[MSSQL_REPL020011](../../relational-databases/replication/mssql-repl020011.md)|O processo não pôde executar '%1' em '%2'.|  
|[MSSQL_REPL027056](../../relational-databases/replication/mssql-repl027056.md)|O processo de mesclagem não pôde alterar o histórico de geração no '%1'. Ao solucionar o problema, reinicie a sincronização com o log de histórico detalhado e especifique um arquivo de saída no qual será realizada a gravação.|  
|[MSSQL_REPL027183](../../relational-databases/replication/mssql-repl027183.md)|O processo de mesclagem não pôde enumerar as alterações nos artigos que apresentaram filtros de linha com parâmetros. Se a falha persistir, aumente o tempo limite da consulta nesse processo, reduza o período de retenção da publicação e aprimore os índices nas tabelas publicadas.|  
  
  
