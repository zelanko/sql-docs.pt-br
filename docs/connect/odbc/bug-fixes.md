---
title: Lista de erros corrigidos | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: genemi
manager: kenvh
ms.workload: Active
ms.openlocfilehash: 58da69ed6c4b7b046f8d1bc1ddf4e23b71b99a29
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="list-of-bugs-fixed"></a>Lista de erros corrigidos

Esta página contém uma lista de erros corrigidos em cada versão, começando com [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17 do Driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>Correções de bug no [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.1 do Driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Corrigido o atraso de 1 segundo ao chamar SQLFreeHandle com MARS ativado e o atributo de conexão "Encrypt = yes"
- Corrigido um travamento de erro 22003 no SQLGetData quando o tamanho do buffer passado é menor, em seguida, os dados que estão sendo recuperados (Windows)
- Fixo mensagens de erro ADAL truncados
- Correção de bug de raro no Windows de 32 bits quando converter um flutuante número de ponto para um número inteiro
- Corrigido um problema em que inserindo duplas no campo decimal com sempre criptografado em retornar erros de truncamento de dados
- Corrigido um aviso no instalador MacOS
- Fixo enviar estado incorreto para o SQL Server durante a tentativa de recuperação da sessão quando a resiliência de Conexão e o Pooling de Conexão ambos estiverem habilitados, fazendo com que a sessão a ser descartado pelo servidor

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>Correções de bug no [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17 do Driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Correção de bug em que ao usar a autenticação Kerberos, a inserção em massa pode falhar com o erro "acesso negado"
- Solução alternativa removida para um bug unixODBC presente na versão abaixo 2.3.1 (driver duplicado os tamanhos de determinados buffers passados para unixODBC)
- Fixo resiliência de Conexão (reconexão) deslocado ao usar ColumnEncryption = habilitado
- Corrigido o bug de criação de DSN, onde quando usando a "Autenticação do Active Directory interativo" a opção autenticação do Azure janela pode tornar-se sem resposta (Windows)
- Corrigido um travamento raro durante o desligamento do ODBC quando a execução assíncrona está habilitada (aconteceu ao limpar o identificador de conexão)
- Corrigido um problema em que o Driver do SQL causado alto consumo de CPU ao executar procedimentos armazenados de longo
- Fixa dificuldades para recuperar dados em uma coluna varbinary (max) criptografado sem conversão
- Corrigido um problema em que após um varchar nulo (max) coluna criptografada é obtida usando SQLGetData() em um cursor estático, a coluna a seguir é também nulled mesmo se ele tiver dados
- Corrigido um problema com a busca de campo varbinary (max) com o sempre criptografado em
- Corrigido um problema de setlocale não está funcionando com o sempre criptografado
- Corrigido um problema com SQLDescribeParam() retornando um erro quando chamado no parâmetro de procedimento armazenado de tipo XML com o sempre criptografado
- Fixos sublinhados com caracteres de escape não está funcionando no SQLTables
- Correção de bug em que os dados hebraicos (varchar) são truncados quando retornados como caracteres largos no Linux
- Corrigido um problema com a consulta Shift-JIS codificado char/varchar do aplicativo de UTF-8
- Corrigido o bug onde chamando SQLGetInfo com parâmetro SQL_DRIVER_NAME retornado filename Linux-style em MacOS
- Corrigido um problema em que o carregamento de dados de caractere do Windows-1252, usando a entrada arquivos maior que 32k bytes em colunas VARCHAR usando o utilitário BCP pode resultar em falhas
