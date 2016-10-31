# Logstash role for Ansible sl_logstash

An Ansible Role that manages Logstash on Debian/Ubuntu/Centos with configuration options for kafka and elasticsearch for use in an ELK stack. Includes options for SSL/TLS 

## Requirements

This module is designed to allow for kafka or elasticsearch outputs and beats inputs

## Role Variables

## The hosts where Logstash should ship logs to Elasticsearch.
    logstash_elasticsearch_hosts:
    - http://localhost:9200

## The hosts where Logstash should ship logs to kafka
    logstash_kafka_hosts:
    - http://localhost:9091

## Logstash plugins
    logstash_install_plugins:
    - logstash-input-beats

## Example Playbook

    - hosts: logstash
      vars_files:
        - vars/secrets.yml 
      roles:
        - sl_logstash

## To use TLS/SSL settings
ssl_enabled: true 
 Include certificates and ensure keys are in PKCS8 format for logstash. encrypt using vault and include in the files specified in the configuration

## example group_vars

    logstash_listen_port_beats: 5044
    beats_in: true
    kafka_out: true
    kafka_in: false
    es_out: false
    kafka_hosts: "kafka-0.example.com, kafka-1.example.com"
    kafka_topic: "mytopic"
    logstash_heap_size: 6g
#SSL
    ssl_enabled: true
    logstash_ssl_dir: /etc/pki/logstash
    logstash_ssl_certificate_file: server.crt
    logstash_ssl_cafile: ca.crt
    logstash_ssl_key_file: server.key

