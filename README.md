rsRaxMon
========
<pre>
rsRaxMon FileSystem
{
    Type = "agent.filesystem"
    Label = "Check Space on System Drive"
    Disabled = "false"
    Period = "60"
    Timeout = "30"
    Target = "C:\"  
    Alarm1_Label = "disk used alarm"
    Alarm1_Plan_ID = "npTechnicalContactsEmail"
    Alarm1_Criteria = "|
                if (percentage(metric['used'], metric['total']) > 90) {
                    return new AlarmStatus(CRITICAL, 'Less than 10% free space left.');
                }
                if (percentage(metric['used'], metric['total']) > 80) {
                    return new AlarmStatus(WARNING, 'Less than 20% free space left.');
                }"
    Alarm2_Label = "disk used alarm"
    Alarm2_Plan_ID = "npTechnicalContactsEmail"
    Alarm2_Criteria  = "|
                if (percentage(metric['used'], metric['total']) > 95) {
                    return new AlarmStatus(CRITICAL, 'Less than 5% free space left.');
                }
                if (percentage(metric['used'], metric['total']) > 90) {
                    return new AlarmStatus(WARNING, 'Less than 10% free space left.');
                }"
    Ensure = "Absent"
    Monitoring_Token = $MonitoringToken
    Monitoring_ID = $MonitoringID
}
</pre>
<pre>
rsRaxMon Http
{
    Type = "remote.http"
    Label = "My Website Check"
    Period = "90"
    Timeout = "30"
    Target_Hostname = "1.2.3.4"
    Url = "http://www.foo.com"
    UrlMethod = "GET"
    Zones_Poll = @("dfw","ord")
    Alarm1_Label = " http connect alarm"
    Alarm1_Plan_ID = "npTechnicalContactsEmail"
    Ensure = "Present"
}
</pre>
<pre>
rsRaxMon CPU
{
    Type = "agent.cpu"
    Label = "CPU"
    Period = "60"
    Timeout = "10"
    Disabled = "false"
    Alarm1_Label = "CPU-Usage"
    Alarm1_Plan_ID = "npTechnicalContactsEmail"
    Alarm1_Criteria = "|
            if (metric['usage_average'] > 95) {
                return new AlarmStatus(CRITICAL, 'CPU usage is #{usage_average}%, above your critical threshold of 95%');
            }
            if (metric['usage_average'] > 90) {
                return new AlarmStatus(WARNING, 'CPU usage is #{usage_average}%, above your warning threshold of 90%');
            }
            return new AlarmStatus(OK, 'CPU usage is #{usage_average}%, below your warning threshold of 90%');"
    Ensure = "Present"
}
</pre>
<pre>
rsRaxMon Memory
{
    Type = "agent.memory"
    Label = "Memory"
    Period = "60"
    Timeout = "30"
    Disabled = "false"
    Alarm1_Label = "High Load Average"
    Alarm1_Plan_ID = "npTechnicalContactsEmail"
    Alarm1_Criteria = "|
        if (percentage(metric['actual_used'], metric['total']) > 90) {
            return new AlarmStatus(CRITICAL, 'Memory usage is above your critical threshold of 90%');
        }
        if (percentage(metric['actual_used'], metric['total']) > 80) {
            return new AlarmStatus(WARNING, 'Memory usage is above your warning threshold of 80%');
        }
        return new AlarmStatus(OK, 'Memory usage is below your warning threshold of 80%');"
    Ensure = "Present"
}
</pre>
<pre>
rsRaxMon Network
{
    Type = "agent.network"
    Label = "Network Check on Public"
    Period = "60"
    Timeout = "30"
    Disabled = "false"
    Target = "public"
    Alarm1_Label = "Network receive rate on public"
    Alarm1_Plan_ID = "npTechnicalContactsEmail"
    Alarm1_Criteria = "|
        if (rate(metric['rx_bytes']) > 76000) {
            return new AlarmStatus(CRITICAL, 'Network receive rate on public is above your critical threshold of 76000B/s');
        }
        if (rate(metric['rx_bytes']) > 56000) {
            return new AlarmStatus(WARNING, 'Network receive rate on public is above your warning threshold of 56000B/s');
        }
        return new AlarmStatus(OK, 'Network receive rate on public is below your warning threshold of 56000B/s');"
    Alarm2_Label = "Network transmit rate on public"
    Alarm2_Plan_ID = "npTechnicalContactsEmail"
    Alarm2_Criteria = "|
        if (rate(metric['tx_bytes']) > 76000) {
            return new AlarmStatus(CRITICAL, 'Network transmit rate on public is above your critical threshold of 76000B/s');
        }
        if (rate(metric['tx_bytes']) > 56000) {
            return new AlarmStatus(WARNING, 'Network transmit rate on public is above your warning threshold of 56000B/s');
        }
        return new AlarmStatus(OK, 'Network transmit rate on public is below your warning threshold of 56000B/s');"
    Ensure = "Present"
}
</pre>