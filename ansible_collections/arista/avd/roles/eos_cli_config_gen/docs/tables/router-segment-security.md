<!--
  ~ Copyright (c) 2024 Arista Networks, Inc.
  ~ Use of this source code is governed by the Apache License 2.0
  ~ that can be found in the LICENSE file.
  -->
=== "Table"

    | Variable | Type | Required | Default | Value Restrictions | Description |
    | -------- | ---- | -------- | ------- | ------------------ | ----------- |
    | [<samp>router_segment_security</samp>](## "router_segment_security") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;enabled</samp>](## "router_segment_security.enabled") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;policies</samp>](## "router_segment_security.policies") | List, items: Dictionary |  |  |  | Customised application policies.<br>Using the Application Traffic Recognition L4 profiles, custom policies can be defined. The built-in application 'app-match-all' can be used to match any packets.<br>Note that this is stateless, so both the source and destination flows need to be considered. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "router_segment_security.policies.[].name") | String | Required, Unique |  |  | Policy name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sequence_numbers</samp>](## "router_segment_security.policies.[].sequence_numbers") | List, items: Dictionary | Required |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;sequence</samp>](## "router_segment_security.policies.[].sequence_numbers.[].sequence") | Integer | Required, Unique |  |  | Sequence ID. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;application</samp>](## "router_segment_security.policies.[].sequence_numbers.[].application") | String | Required |  |  | The name of the application. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;action</samp>](## "router_segment_security.policies.[].sequence_numbers.[].action") | String | Required |  | Valid Values:<br>- <code>forward</code><br>- <code>drop</code><br>- <code>redirect</code> | The action to take - note that platform support for the redirect action is limited. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log</samp>](## "router_segment_security.policies.[].sequence_numbers.[].log") | Boolean |  |  |  | Enable logging - note that platform support is limited. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stateless</samp>](## "router_segment_security.policies.[].sequence_numbers.[].stateless") | Boolean |  | `True` |  | Take action, regardless of state. Should be set to 'true' for MSS-G. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;next_hop</samp>](## "router_segment_security.policies.[].sequence_numbers.[].next_hop") | String |  |  |  | When the action is 'redirect', this indicates the IPv4 next hop to redirect to. |
    | [<samp>&nbsp;&nbsp;vrfs</samp>](## "router_segment_security.vrfs") | List, items: Dictionary |  |  |  | The name of the VRF that the segments and policies are defined in. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "router_segment_security.vrfs.[].name") | String | Required, Unique |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;segments</samp>](## "router_segment_security.vrfs.[].segments") | List, items: Dictionary | Required |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "router_segment_security.vrfs.[].segments.[].name") | String | Required, Unique |  |  | Segment name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;definition</samp>](## "router_segment_security.vrfs.[].segments.[].definition") | Dictionary | Required |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;interfaces</samp>](## "router_segment_security.vrfs.[].segments.[].definition.interfaces") | List, items: String |  |  | Min Length: 1 | The names of the source interface e.g. Port-Channel1 - note that platform support is limited. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "router_segment_security.vrfs.[].segments.[].definition.interfaces.[]") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;match_lists</samp>](## "router_segment_security.vrfs.[].segments.[].definition.match_lists") | List, items: Dictionary |  |  | Min Length: 1<br>Max Length: 2 | The set of lists that define the segment. These can be a mix of IPv4 and IPv6 prefix or match lists. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;address_family</samp>](## "router_segment_security.vrfs.[].segments.[].definition.match_lists.[].address_family") | String | Required, Unique |  | Valid Values:<br>- <code>ipv4</code><br>- <code>ipv6</code> | Indicate which address-family the match list belongs to e.g. ipv4 or ipv6. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;covered_prefix_list</samp>](## "router_segment_security.vrfs.[].segments.[].definition.match_lists.[].covered_prefix_list") | String |  |  |  | The name of the prefix-list. You can have a maximum of one per address-family. Mutually exclusive to the use of match_list.  If both are configured prefix takes precedence. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;prefix</samp>](## "router_segment_security.vrfs.[].segments.[].definition.match_lists.[].prefix") | String |  |  |  | The name of the match-list. You can have a maximum of one per address-family. Mutually exclusive to the use of covered_prefix_list. If both are configured prefix takes precedence. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;policies</samp>](## "router_segment_security.vrfs.[].segments.[].policies") | List, items: Dictionary | Required |  |  | The policies controlling traffic into the segment. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;source</samp>](## "router_segment_security.vrfs.[].segments.[].policies.[].source") | String | Required, Unique |  |  | The name of the source segment. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;policy</samp>](## "router_segment_security.vrfs.[].segments.[].policies.[].policy") | String |  |  |  | The name of the policy to apply. The built-in policies are 'policy-forward-all' and 'policy-drop-all'. |

=== "YAML"

    ```yaml
    router_segment_security:
      enabled: <bool>

      # Customised application policies.
      # Using the Application Traffic Recognition L4 profiles, custom policies can be defined. The built-in application 'app-match-all' can be used to match any packets.
      # Note that this is stateless, so both the source and destination flows need to be considered.
      policies:

          # Policy name.
        - name: <str; required; unique>
          sequence_numbers: # required

              # Sequence ID.
            - sequence: <int; required; unique>

              # The name of the application.
              application: <str; required>

              # The action to take - note that platform support for the redirect action is limited.
              action: <str; "forward" | "drop" | "redirect"; required>

              # Enable logging - note that platform support is limited.
              log: <bool>

              # Take action, regardless of state. Should be set to 'true' for MSS-G.
              stateless: <bool; default=True>

              # When the action is 'redirect', this indicates the IPv4 next hop to redirect to.
              next_hop: <str>

      # The name of the VRF that the segments and policies are defined in.
      vrfs:
        - name: <str; required; unique>
          segments: # required

              # Segment name.
            - name: <str; required; unique>
              definition: # required

                # The names of the source interface e.g. Port-Channel1 - note that platform support is limited.
                interfaces: # >=1 items
                  - <str>

                # The set of lists that define the segment. These can be a mix of IPv4 and IPv6 prefix or match lists.
                match_lists: # 1-2 items

                    # Indicate which address-family the match list belongs to e.g. ipv4 or ipv6.
                  - address_family: <str; "ipv4" | "ipv6"; required; unique>

                    # The name of the prefix-list. You can have a maximum of one per address-family. Mutually exclusive to the use of match_list.  If both are configured prefix takes precedence.
                    covered_prefix_list: <str>

                    # The name of the match-list. You can have a maximum of one per address-family. Mutually exclusive to the use of covered_prefix_list. If both are configured prefix takes precedence.
                    prefix: <str>

              # The policies controlling traffic into the segment.
              policies: # required

                  # The name of the source segment.
                - source: <str; required; unique>

                  # The name of the policy to apply. The built-in policies are 'policy-forward-all' and 'policy-drop-all'.
                  policy: <str>
    ```