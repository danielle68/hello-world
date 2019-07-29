# hello-world
just another repository


O agente Zabbix deve ser executado no host que se deseja monitorar. O agente Zabbix é executado como um processo daemon.

* Para iniciar o agente, execute:

  shell> cd sbin
  shell> ./zabbix_agentd
 
 * São possíveis alguns parâmetros na linha de comando do agente:

 # -c --config <arquivo>           caminho absoluto (completo) para o arquivo de configuração (o padrão é /etc/zabbix/zabbix_agentd.conf)
  #-R --runtime-control <opção>    executa funções administrativas
  #-h --help            apresenta o help de parâmetros
  #-V --version         apresenta o número de versão
  #-p --print           apresenta todos os itens (chaves) possíveis
  #-t --test <chave do item> testa um item específico e retorna o resultado
  
  
 *  Para obter este help, execute:

shell> zabbix_agentd -h

* Outros exemplos com os parâmetros em linha de comando:

shell> zabbix_agentd -c /usr/local/etc/zabbix_agentd.conf
shell> zabbix_agentd --help
shell> zabbix_agentd --print
shell> zabbix_agentd -t "system.cpu.load[all,avg1]"
Controle em tempo de execução

* Opções de controle em tempo de execução:

Opção	Descrição	Alvo
log_level_increase[=<alvo>]	Aumenta o nível de log, afeta todos os processos se o alvo não for especificado.	pid - Identificador do processo (1 a 65535) 
tipo do processo - Restringe a todos os processos de determinado tipo (Ex.: poller) 
tipo do processo,N - Restringe a determinado processo de um tipo específico (Ex.: poller,3)
log_level_decrease[=<alvo>]	Reduz o nível de log, afeta todos os processos se o alvo não for especificado.
O PID do processo a se modificar o nível de log deverá estar entre 1 e 65535. Em ambientes com muitos processos a modificação poderá ser feita em um processo específico.

* Exemplo de utilização do controle em tempo de execução para modificar o nível de log:

# Increase log level of all processes:
# shell> zabbix_agentd -c /usr/local/etc/zabbix_agentd.conf -R log_level_increase

# Aumenta o nível de log do segundo processo do ouvinte (listener):
# shell> zabbix_agentd -c /usr/local/etc/zabbix_agentd.conf -R log_level_increase=listener,2

# Aumenta o nível de log do processo com PID 1234:
# shell> zabbix_agentd -c /usr/local/etc/zabbix_agentd.conf -R log_level_increase=1234

# Reduz o nível de log de todas os processos de verificação ativa:
# shell> zabbix_agentd -c /usr/local/etc/zabbix_agentd.conf -R log_level_decrease="active checks"
# Processo de usuário

* O agente Zabbix foi desenhado para ser executado como um processo “não-root”. Ele pode ser executado com a permissão do usuário que o iniciou. Neste cenário ele irá executar sem nenhum problema.

Se você tentar inicia-lo com o usuário 'root', ele alternará seu permissionamento de execução para o usuário 'zabbix', que deverá existir em seu ambiente. Você só poderá rodar o Servidor Zabbix como 'root' se modificar o parâmetro 'AllowRoot' no arquivo de configuração.

* Arquivo de configuração
Veja as opções do arquivo de configuração para detalhes sobre sua configuração.

Executando o agente em ambiente Microsoft Windows
Veja o manual do agente no Windows para detalhes sobre como instalar, configurar e executar o agente neste sistema operacional.

Sintaxe de linha de comando do agente no Windows:

# zabbix_agentd.exe [-c arquivo-de-configuração]
# zabbix_agentd.exe [-c arquivo-de-configuração] -p
# zabbix_agentd.exe [-c arquivo-de-configuração] -t chave-do-item
# zabbix_agentd.exe [-c arquivo-de-configuração] -i [-m]
# zabbix_agentd.exe [-c arquivo-de-configuração] -d [-m]
# zabbix_agentd.exe [-c arquivo-de-configuração] -s [-m]
# zabbix_agentd.exe [-c arquivo-de-configuração] -x [-m]
# zabbix_agentd.exe -h
# zabbix_agentd.exe -V

* Os parâmetros a seguir podem ser utilizados.

Options:

  # -c --config <arquivo>           caminho absoluto (completo) para o arquivo de configuração (o padrão é c:\zabbix_agentd.conf)
  # -h --help            apresenta o help de parâmetros
  # -V --version         apresenta o número de versão
  # -p --print           apresenta todos os itens (chaves) possíveis
  # -t --test <chave do item> testa um item específico e retorna o resultado
Functions:
  # -i --install          Instala o serviço do agente Zabbix
  # -d --uninstall        Desinstala o serviço do agente Zabbis
  # -s --start            Inicia o serviço do agente Zabbix
  # -x --stop             Finaliza o serviço do agente Zabbix
  # -m --multiple-agents  Nome do serviço com o hostname
  
* Arquivo de configuração
Veja o manual do arquivo de configuração para detalhes de opções de configuração do agente Zabbix no Windows.

Códigos de saída
Antes da versão 2.2 do Zabbix o agente retornava 0 em caso de sucesso e 255 em caso de falha. A partir desta versão o agente passou a retornar 0 para sucesso e 1 para falha.
