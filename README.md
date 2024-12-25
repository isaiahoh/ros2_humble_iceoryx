# ROS2 Humble Iceoryx Issue

## Environment:

- OS: Ubuntu 22.04
- ROS2: Humble
- rmw_iceoryx_cpp: branch humble
- iceoryx: branch v2.0.3

## Issue:

When running the lifecycle_talker node with the rmw_iceoryx_cpp implementation, the node crashes with a segmentation fault when the lifecycle_set node is run to configure the lifecycle_talker node.

```
Log level set to: [Warning]
Segmentation fault (core dumped)
```

## Expected Behavior:

The lifecycle_talker node should not crash when the lifecycle_set node is run to configure the lifecycle_talker node.

## Pre-requisites:

1. clone this repository:

```bash
git clone https://github.com/isaiahoh/ros2_humble_iceoryx.git
```

2. init and update the submodules:

```bash
cd ros2_humble_iceoryx
git submodule update --init --recursive
```

3. build the workspace:

```bash
colcon build
```

## Steps to Reproduce:

Open 3 terminals in the workspace directory.

1. Run the following command in the first terminal (iox-roudi-terminal):

```bash
source install/setup.bash
iox-roudi -l verbose -m off
```

2. Run the following command in the second terminal (lifecycle_talker-terminal):

```bash
source install/setup.bash
RMW_IMPLEMENTATION=rmw_iceoryx_cpp ros2 run lifecycle_demo lifecycle_talker
```

3. Run the following command in the third terminal (lifecycle_set-terminal):

```bash
source install/setup.bash
RMW_IMPLEMENTATION=rmw_iceoryx_cpp ros2 lifecycle set /lifecycle_talker configure
```

Outputs:

1. iox-roudi-terminal:

```bash
2024-12-25 11:24:39.033 [ Info  ]: No config file provided and also not found at '/etc/iceoryx/roudi_config.toml'. Falling back to built-in config.
Log level set to: [Verbose]
2024-12-25 11:24:39.033 [Verbose]: Command line parameters are:
Log level: Verbose
Monitoring mode: MonitoringMode::OFF
Compatibility check level: CompatibilityCheckLevel::PATCH
Unique RouDi ID: < unset >
Process kill delay: 45 s
Config file used is: < none >
Reserving 66761736 bytes in the shared memory [iceoryx_mgmt]
[ Reserving shared memory successful ]
2024-12-25 11:24:39.088 [ Debug ]: Registered memory segment 0x7fefc9454000 with size 66761736 to id 1
Reserving 149264720 bytes in the shared memory [isaiah]
[ Reserving shared memory successful ]
2024-12-25 11:24:39.202 [ Debug ]: Roudi registered payload data segment 0x7fefc05fa000 with size 149264720 to id 2
RouDi is ready for clients
2024-12-25 11:25:12.565 [ Debug ]: Registered new application lifecycle_talker_389265
2024-12-25 11:25:12.567 [ Debug ]: Created new ConditionVariable for application lifecycle_talker_389265
2024-12-25 11:25:12.568 [ Debug ]: Created new SubscriberPort for application 'lifecycle_talker_389265' with service description 'Service: Introspection, Instance: RouDi_ID, Event: Port'
2024-12-25 11:25:12.568 [ Debug ]: Created new ConditionVariable for application lifecycle_talker_389265
2024-12-25 11:25:12.568 [ Debug ]: Created new node /lifecycle_talker for process lifecycle_talker_389265
2024-12-25 11:25:12.569 [ Debug ]: Created new PublisherPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/msg/Log, Instance: /rosout, Event: data'
2024-12-25 11:25:12.569 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/srv/GetParameters, Instance: /lifecycle_talker/get_parameters, Event: data'
2024-12-25 11:25:12.569 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/srv/GetParameterTypes, Instance: /lifecycle_talker/get_parameter_types, Event: data'
2024-12-25 11:25:12.570 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/srv/SetParameters, Instance: /lifecycle_talker/set_parameters, Event: data'
2024-12-25 11:25:12.570 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/srv/SetParametersAtomically, Instance: /lifecycle_talker/set_parameters_atomically, Event: data'
2024-12-25 11:25:12.570 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/srv/DescribeParameters, Instance: /lifecycle_talker/describe_parameters, Event: data'
2024-12-25 11:25:12.571 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/srv/ListParameters, Instance: /lifecycle_talker/list_parameters, Event: data'
2024-12-25 11:25:12.571 [ Debug ]: Created new PublisherPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/msg/ParameterEvent, Instance: /parameter_events, Event: data'
2024-12-25 11:25:12.571 [ Debug ]: Created new SubscriberPort for application 'lifecycle_talker_389265' with service description 'Service: rcl_interfaces/msg/ParameterEvent, Instance: /parameter_events, Event: data'
2024-12-25 11:25:12.572 [ Debug ]: Created new PublisherPort for application 'lifecycle_talker_389265' with service description 'Service: lifecycle_msgs/msg/TransitionEvent, Instance: /lifecycle_talker/transition_event, Event: data'
2024-12-25 11:25:12.572 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: lifecycle_msgs/srv/ChangeState, Instance: /lifecycle_talker/change_state, Event: data'
2024-12-25 11:25:12.572 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: lifecycle_msgs/srv/GetState, Instance: /lifecycle_talker/get_state, Event: data'
2024-12-25 11:25:12.573 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: lifecycle_msgs/srv/GetAvailableStates, Instance: /lifecycle_talker/get_available_states, Event: data'
2024-12-25 11:25:12.573 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: lifecycle_msgs/srv/GetAvailableTransitions, Instance: /lifecycle_talker/get_available_transitions, Event: data'
2024-12-25 11:25:12.573 [ Debug ]: Created new ServerPort for application 'lifecycle_talker_389265' with service description 'Service: lifecycle_msgs/srv/GetAvailableTransitions, Instance: /lifecycle_talker/get_transition_graph, Event: data'
2024-12-25 11:25:43.059 [ Debug ]: Registered new application python3_389355
2024-12-25 11:25:43.061 [ Debug ]: Created new SubscriberPort for application 'python3_389355' with service description 'Service: Introspection, Instance: RouDi_ID, Event: Port'
2024-12-25 11:25:43.061 [ Debug ]: Created new ConditionVariable for application python3_389355
2024-12-25 11:25:43.061 [ Debug ]: Created new node /_ros2cli_389355 for process python3_389355
2024-12-25 11:25:43.080 [ Debug ]: Created new PublisherPort for application 'python3_389355' with service description 'Service: rcl_interfaces/msg/Log, Instance: /rosout, Event: data'
2024-12-25 11:25:43.123 [ Debug ]: Created new PublisherPort for application 'python3_389355' with service description 'Service: rcl_interfaces/msg/ParameterEvent, Instance: /parameter_events, Event: data'
2024-12-25 11:25:43.125 [ Debug ]: Created new ConditionVariable for application python3_389355
2024-12-25 11:25:43.388 [ Debug ]: Registered new application python3_389356
2024-12-25 11:25:43.389 [ Debug ]: Created new SubscriberPort for application 'python3_389356' with service description 'Service: Introspection, Instance: RouDi_ID, Event: Port'
2024-12-25 11:25:43.389 [ Debug ]: Created new ConditionVariable for application python3_389356
2024-12-25 11:25:43.390 [ Debug ]: Created new node /_ros2cli_daemon_0_0aa4ab19a3da4f9087255a789a476eb3 for process python3_389356
2024-12-25 11:25:43.390 [ Debug ]: Created new PublisherPort for application 'python3_389356' with service description 'Service: rcl_interfaces/msg/Log, Instance: /rosout, Event: data'
2024-12-25 11:25:43.428 [ Debug ]: Created new PublisherPort for application 'python3_389356' with service description 'Service: rcl_interfaces/msg/ParameterEvent, Instance: /parameter_events, Event: data'
2024-12-25 11:25:43.429 [ Debug ]: Created new ConditionVariable for application python3_389356
2024-12-25 11:25:43.625 [ Debug ]: Created new SubscriberPort for application 'python3_389355' with service description 'Service: Introspection, Instance: RouDi_ID, Event: Process'
2024-12-25 11:25:43.626 [ Debug ]: Created new SubscriberPort for application 'python3_389355' with service description 'Service: ServiceDiscovery, Instance: RouDi_ID, Event: ServiceRegistry'
2024-12-25 11:25:43.629 [ Debug ]: Created new SubscriberPort for application 'python3_389355' with service description 'Service: Introspection, Instance: RouDi_ID, Event: Port'
2024-12-25 11:25:43.629 [ Debug ]: Created new ConditionVariable for application python3_389355
2024-12-25 11:25:43.629 [Warning]: Node /_ros2cli_389355 already registered
2024-12-25 11:25:43.629 [ Debug ]: Created new node /_ros2cli_389355 for process python3_389355
2024-12-25 11:25:43.630 [ Debug ]: Created new PublisherPort for application 'python3_389355' with service description 'Service: rcl_interfaces/msg/Log, Instance: /rosout, Event: data'
2024-12-25 11:25:43.631 [ Debug ]: Created new PublisherPort for application 'python3_389355' with service description 'Service: rcl_interfaces/msg/ParameterEvent, Instance: /parameter_events, Event: data'
2024-12-25 11:25:43.633 [ Debug ]: Created new ConditionVariable for application python3_389355
2024-12-25 11:25:43.702 [ Debug ]: Destroy publisher port from runtime 'python3_389355' and with service description 'Service: rcl_interfaces/msg/Log, Instance: /rosout, Event: data'
2024-12-25 11:25:43.703 [ Debug ]: Destroy publisher port from runtime 'python3_389355' and with service description 'Service: rcl_interfaces/msg/ParameterEvent, Instance: /parameter_events, Event: data'
2024-12-25 11:25:43.703 [ Debug ]: Destroy subscriber port from runtime 'python3_389355' and with service description 'Service: Introspection, Instance: RouDi_ID, Event: Port'
2024-12-25 11:25:43.703 [ Debug ]: Destroy subscriber port from runtime 'python3_389355' and with service description 'Service: ServiceDiscovery, Instance: RouDi_ID, Event: ServiceRegistry'
2024-12-25 11:25:43.703 [ Debug ]: Destroy NodeData from runtime 'python3_389355' and node name '/_ros2cli_389355'
2024-12-25 11:25:43.703 [ Debug ]: Destroy ConditionVariableData from runtime 'python3_389355'
2024-12-25 11:25:43.703 [ Debug ]: Destroy ConditionVariableData from runtime 'python3_389355'
2024-12-25 11:25:44.146 [ Debug ]: Created new ClientPort for application 'python3_389355' with service description 'Service: lifecycle_msgs/srv/GetAvailableTransitions, Instance: /lifecycle_talker/get_available_transitions, Event: data'
2024-12-25 11:25:45.147 [ Debug ]: Created new ConditionVariable for application python3_389355
2024-12-25 11:25:45.205 [ Debug ]: Destroy ConditionVariableData from runtime 'python3_389355'

```

2. lifecycle_talker-terminal:

```bash
Log level set to: [Warning]
2024-12-25 11:25:12.571 [Warning]: Requested queue capacity 1000 exceeds the maximum possible one for this subscriber, limiting from 1000 to 256
```

3. lifecycle_set-terminal:

```bash
Log level set to: [Warning]
Segmentation fault (core dumped)
```

## Additional Information:

- lifecycle_set-terminal with gdb:

```bash
RMW_IMPLEMENTATION=rmw_iceoryx_cpp gdb -ex r --args python3 `which ros2` lifecycle set /lifecycle_talker configure
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from python3...
Reading symbols from /usr/lib/debug/.build-id/64/a3ce48961c34435d35fee80c3dc016dc04b469.debug...
Starting program: /usr/bin/python3 /opt/ros/humble/bin/ros2 lifecycle set /lifecycle_talker configure
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
Log level set to: [Warning]
[New Thread 0x7fffe6a00640 (LWP 392998)]
[New Thread 0x7fffe6000640 (LWP 392999)]
[New Thread 0x7fffe5600640 (LWP 393000)]

Thread 1 "python3" received signal SIGSEGV, Segmentation fault.
0x00007ffff5c9edfe in char const* rmw_iceoryx_cpp::details_c::deserialize_element<unsigned char, 1ul>(char const*, void*) () from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
(gdb) backtrace
#0  0x00007ffff5c9edfe in char const* rmw_iceoryx_cpp::details_c::deserialize_element<unsigned char, 1ul>(char const*, void*)
    () from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
#1  0x00007ffff5c9d4eb in char const* rmw_iceoryx_cpp::details_c::deserialize_message_field<unsigned char>(rosidl_typesupport_introspection_c__MessageMember_s const*, char const*, void*) ()
   from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
#2  0x00007ffff5c9ba3f in rmw_iceoryx_cpp::details_c::deserialize(char const*, rosidl_typesupport_introspection_c__MessageMembers_s const*, void*) () from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
#3  0x00007ffff5c9bce2 in rmw_iceoryx_cpp::details_c::deserialize(char const*, rosidl_typesupport_introspection_c__MessageMembers_s const*, void*) () from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
#4  0x00007ffff5c9bce2 in rmw_iceoryx_cpp::details_c::deserialize(char const*, rosidl_typesupport_introspection_c__MessageMembers_s const*, void*) () from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
#5  0x00007ffff5c9bdd0 in rmw_iceoryx_cpp::details_c::deserializeResponse(char const*, rosidl_typesupport_introspection_c__ServiceMembers_s const*, void*) ()
   from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
#6  0x00007ffff5c9c946 in rmw_iceoryx_cpp::deserializeResponse(char const*, rosidl_service_type_support_t const*, void*) ()
   from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_serialization.so
#7  0x00007ffff5d4846a in rmw_take_response::{lambda(void const*)#1}::operator()(void const*) const ()
   from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_cpp.so
#8  0x00007ffff5d4924b in iox::cxx::function_ref<void (void const*&)>::function_ref<rmw_take_response::{lambda(void const*)#1}, void>(rmw_take_response::{lambda(void const*)#1}&&)::{lambda(void*, void const*&)#1}::operator()(void*, void const*&) const
    () from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_cpp.so
#9  0x00007ffff5d4927b in iox::cxx::function_ref<void (void const*&)>::function_ref<rmw_take_response::{lambda(void const*)#1}, void>(rmw_take_response::{lambda(void const*)#1}&&)::{lambda(void*, void const*&)#1}::_FUN(void*, void const*&) ()
   from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_cpp.so
#10 0x00007ffff5d4040b in iox::cxx::function_ref<void (void const*&)>::operator()(void const*&) const ()
   from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_cpp.so
#11 0x00007ffff5d3fbe3 in iox::cxx::expected<void const*, iox::popo::ChunkReceiveResult>::and_then(iox::cxx::function_ref<void (void const*&)> const&) () from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_cpp.so
#12 0x00007ffff5d48920 in rmw_take_response ()
--Type <RET> for more, q to quit, c to continue without paging--
   from /home/user/ros2_humble_iceoryx/install/rmw_iceoryx_cpp/lib/librmw_iceoryx_cpp.so
#13 0x00007ffff64e276d in rcl_take_response_with_info () from /opt/ros/humble/lib/librcl.so
#14 0x00007ffff659ca79 in ?? ()
   from /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/_rclpy_pybind11.cpython-310-x86_64-linux-gnu.so
#15 0x00007ffff659a396 in ?? ()
   from /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/_rclpy_pybind11.cpython-310-x86_64-linux-gnu.so
#16 0x00007ffff65791b9 in ?? ()
   from /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/_rclpy_pybind11.cpython-310-x86_64-linux-gnu.so
#17 0x00005555556df282 in cfunction_call (func=<built-in method take_response of PyCapsule object at remote 0x7ffff665aaf0>,
    args=<optimized out>, kwargs=<optimized out>) at ../Objects/methodobject.c:543
#18 0x00005555556d5b4b in _PyObject_MakeTpCall (tstate=0x555555b63240,
    callable=<built-in method take_response of PyCapsule object at remote 0x7ffff665aaf0>, args=<optimized out>,
    nargs=<optimized out>, keywords=0x0) at ../Objects/call.c:215
#19 0x00005555556ecebb in _PyObject_VectorcallTstate (kwnames=<optimized out>, nargsf=<optimized out>, args=0x7fffe4dbd210,
    callable=<built-in method take_response of PyCapsule object at remote 0x7ffff665aaf0>, tstate=0x555555b63240)
    at ../Include/cpython/abstract.h:112
#20 _PyObject_VectorcallTstate (kwnames=<optimized out>, nargsf=<optimized out>, args=0x7fffe4dbd210,
    callable=<built-in method take_response of PyCapsule object at remote 0x7ffff665aaf0>, tstate=0x555555b63240)
    at ../Include/cpython/abstract.h:99
#21 method_vectorcall (method=<optimized out>, args=0x7fffe4dbd218, nargsf=<optimized out>, kwnames=<optimized out>)
    at ../Objects/classobject.c:53
#22 0x00005555556ceb7a in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4dbd218,
    callable=<method at remote 0x7ffff6661900>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#23 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4dbd218, callable=<method at remote 0x7ffff6661900>)
    at ../Include/cpython/abstract.h:123
#24 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffbbf0,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#25 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4181
#26 0x00005555556ecbe1 in _PyEval_EvalFrame (throwflag=0,
--Type <RET> for more, q to quit, c to continue without paging--
    f=Frame 0x7fffe4dbd090, for file /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/executors.py, line 366, in _take_client (self=<SingleThreadedExecutor(_context=<Context(_lock=<_thread.lock at remote 0x7ffff3975dc0>, _callbacks=[<WeakMethod at remote 0x7fffe4d347b0>, <function at remote 0x7ffff397aa70>], _logging_initialized=True, _Context__context=<rclpy._rclpy_pybind11.Context at remote 0x7ffff3975cf0>) at remote 0x7ffff3ac8f40>, _nodes={<DirectNode(node=<Node(_Node__handle=None, _context=<...>, _parameters={'use_sim_time': <Parameter(_type_=<Type(_value_=1, _name_='BOOL', __objclass__=<EnumMeta(_generate_next_value_=<function at remote 0x7ffff6ae9360>, __module__='rclpy.parameter', from_parameter_value=<classmethod at remote 0x7ffff673d7e0>, check=<function at remote 0x7ffff664ce50>, __doc__='An enumeration.', _member_names_=['NOT_SET', 'BOOL', 'INTEGER', 'DOUBLE', 'STRING', 'BYTE_ARRAY', 'BOOL_ARRAY', 'INTEGER_ARRAY', 'DOUBLE_ARRAY', 'STRING_ARRAY'], _member_map_={'NOT_SET': <Type(_value_=0, _name_=...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#27 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=0x7ffff3a7b3e0, locals=0x0, con=0x7ffff57aa0f0,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#28 _PyFunction_Vectorcall (kwnames=<optimized out>, nargsf=<optimized out>, stack=0x7ffff3a7b3e0,
    func=<function at remote 0x7ffff57aa0e0>) at ../Objects/call.c:342
#29 _PyObject_VectorcallTstate (kwnames=<optimized out>, nargsf=<optimized out>, args=0x7ffff3a7b3e0,
    callable=<function at remote 0x7ffff57aa0e0>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#30 method_vectorcall (method=<optimized out>, args=0x7ffff3a7b3e8, nargsf=<optimized out>, kwnames=<optimized out>)
    at ../Objects/classobject.c:53
#31 0x00005555556c99a2 in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7ffff3a7b3e8,
    callable=<method at remote 0x7ffff4384340>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#32 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7ffff3a7b3e8, callable=<method at remote 0x7ffff4384340>)
    at ../Include/cpython/abstract.h:123
#33 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffbe30,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#34 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4213
#35 0x00005555556fbb40 in _PyEval_EvalFrame (throwflag=<optimized out>,
    f=Frame 0x7ffff3a7b240, for file /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/executors.py, line 430, in handler (entity=<Client(context=<Context(_lock=<_thread.lock at remote 0x7ffff3975dc0>, _callbacks=[<WeakMethod at remote 0x7fffe4d347b0>, <function at remote 0x7ffff397aa70>], _logging_initialized=True, _Context__context=<rclpy._rclpy_pybind11.Context at remote 0x7ffff3975cf0>) at remote 0x7ffff3ac8f40>, _Client__client=<rclpy._rclpy_pybind11.Client at remote 0x7fffe4d9ff70>, srv_typ--Type <RET> for more, q to quit, c to continue without paging--
e=<Metaclass_GetAvailableTransitions(__module__='lifecycle_msgs.srv._get_available_transitions', Request=<Metaclass_GetAvailableTransitions_Request(__module__='lifecycle_msgs.srv._get_available_transitions', __doc__="Message class 'GetAvailableTransitions_Request'.", __slots__=[], _fields_and_field_types={}, SLOT_TYPES=(), __init__=<function at remote 0x7ffff3ab5240>, __repr__=<function at remote 0x7ffff3ab52d0>, __eq__=<function at remote 0x7ffff3ab5360>, get_fields_and_field_types=<classmethod at remote 0x7ffff3ac5...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#36 gen_send_ex2 (gen=0x7fffe4d7f300, arg=None, presult=0x7fffffffbf08, exc=<optimized out>, closing=<optimized out>)
    at ../Objects/genobject.c:213
#37 0x00005555557cc6df in gen_send_ex (gen=0x7fffe4d7f300, arg=<optimized out>, exc=<optimized out>, closing=<optimized out>)
    at ../Objects/genobject.c:279
#38 0x00005555556ea78b in method_vectorcall_O (func=<optimized out>, args=0x7fffe4db4578, nargsf=<optimized out>, kwnames=0x0)
    at ../Objects/descrobject.c:460
#39 0x00005555556c9ae8 in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db4578,
    callable=<method_descriptor at remote 0x7ffff6d27510>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#40 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db4578,
    callable=<method_descriptor at remote 0x7ffff6d27510>) at ../Include/cpython/abstract.h:123
#41 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffc070,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#42 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4198
#43 0x00005555556d4d14 in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7fffe4db4400, for file /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/task.py, line 239, in __call__ (self=<Task(_done=False, _cancelled=False, _result=None, _exception=None, _exception_fetched=False, _callbacks=[], _lock=<_thread.lock at remote 0x7ffff667e680>, _executor=<weakref.ReferenceType at remote 0x7fffe4d99990>, _handler=<coroutine at remote 0x7fffe4d7f300>, _args=None, _kwargs=None, _executing=True, _task_lock=<_thread.lock at remote 0x7ffff667c600>) at remote 0x7fffe4ddc1f0>), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#44 _PyEval_Vector (kwnames=0x0, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff664fbf0,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#45 _PyFunction_Vectorcall (kwnames=0x0, nargsf=<optimized out>, stack=<optimized out>,
    func=<function at remote 0x7ffff664fbe0>) at ../Objects/call.c:342
#46 _PyObject_FastCallDictTstate (tstate=0x555555b63240, callable=<function at remote 0x7ffff664fbe0>, args=<optimized out>,
--Type <RET> for more, q to quit, c to continue without paging--
    nargsf=<optimized out>, kwargs=<optimized out>) at ../Objects/call.c:142
#47 0x00005555556e9d4c in _PyObject_Call_Prepend (tstate=0x555555b63240, callable=<function at remote 0x7ffff664fbe0>,
    obj=<optimized out>, args=<optimized out>, kwargs=0x0) at ../Objects/call.c:431
#48 0x00005555557f2054 in slot_tp_call (
    self=<Task(_done=False, _cancelled=False, _result=None, _exception=None, _exception_fetched=False, _callbacks=[], _lock=<_thread.lock at remote 0x7ffff667e680>, _executor=<weakref.ReferenceType at remote 0x7fffe4d99990>, _handler=<coroutine at remote 0x7fffe4d7f300>, _args=None, _kwargs=None, _executing=True, _task_lock=<_thread.lock at remote 0x7ffff667c600>) at remote 0x7fffe4ddc1f0>, args=(), kwds=0x0) at ../Objects/typeobject.c:7494
#49 0x00005555556d5b4b in _PyObject_MakeTpCall (tstate=0x555555b63240,
    callable=<Task(_done=False, _cancelled=False, _result=None, _exception=None, _exception_fetched=False, _callbacks=[], _lock=<_thread.lock at remote 0x7ffff667e680>, _executor=<weakref.ReferenceType at remote 0x7fffe4d99990>, _handler=<coroutine at remote 0x7fffe4d7f300>, _args=None, _kwargs=None, _executing=True, _task_lock=<_thread.lock at remote 0x7ffff667c600>) at remote 0x7fffe4ddc1f0>, args=<optimized out>, nargs=<optimized out>, keywords=0x0) at ../Objects/call.c:215
#50 0x00005555556cef4d in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db43b0,
    callable=<optimized out>, tstate=<optimized out>) at ../Include/cpython/abstract.h:112
#51 _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db43b0, callable=<optimized out>,
    tstate=<optimized out>) at ../Include/cpython/abstract.h:99
#52 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db43b0, callable=<optimized out>)
    at ../Include/cpython/abstract.h:123
#53 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffc3b0,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#54 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4213
#55 0x00005555556dfaec in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7fffe4db4220, for file /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/executors.py, line 734, in _spin_once_impl (self=<SingleThreadedExecutor(_context=<Context(_lock=<_thread.lock at remote 0x7ffff3975dc0>, _callbacks=[<WeakMethod at remote 0x7fffe4d347b0>, <function at remote 0x7ffff397aa70>], _logging_initialized=True, _Context__context=<rclpy._rclpy_pybind11.Context at remote 0x7ffff3975cf0>) at remote 0x7ffff3ac8f40>, _nodes={<DirectNode(node=<Node(_Node__handle=None, _context=<...>, _parameters={'use_sim_time': <Parameter(_type_=<Type(_value_=1, _name_='BOOL', __objclass__=<EnumMeta(_generate_next_value_=<function at remote 0x7ffff6ae9360>, __module__='rclpy.parameter', from_parameter_value=<classmethod at remote 0x7ffff67--Type <RET> for more, q to quit, c to continue without paging--
3d7e0>, check=<function at remote 0x7ffff664ce50>, __doc__='An enumeration.', _member_names_=['NOT_SET', 'BOOL', 'INTEGER', 'DOUBLE', 'STRING', 'BYTE_ARRAY', 'BOOL_ARRAY', 'INTEGER_ARRAY', 'DOUBLE_ARRAY', 'STRING_ARRAY'], _member_map_={'NOT_SET': <Type(_value_=0, _nam...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#56 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff57aa840,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#57 _PyFunction_Vectorcall (func=<function at remote 0x7ffff57aa830>, stack=<optimized out>, nargsf=<optimized out>,
    kwnames=<optimized out>) at ../Objects/call.c:342
#58 0x00005555556c9ae8 in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db12a0,
    callable=<function at remote 0x7ffff57aa830>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#59 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db12a0,
    callable=<function at remote 0x7ffff57aa830>) at ../Include/cpython/abstract.h:123
#60 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffc590,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#61 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4198
#62 0x00005555556dfaec in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7fffe4db1120, for file /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/executors.py, line 746, in spin_once_until_future_complete (self=<SingleThreadedExecutor(_context=<Context(_lock=<_thread.lock at remote 0x7ffff3975dc0>, _callbacks=[<WeakMethod at remote 0x7fffe4d347b0>, <function at remote 0x7ffff397aa70>], _logging_initialized=True, _Context__context=<rclpy._rclpy_pybind11.Context at remote 0x7ffff3975cf0>) at remote 0x7ffff3ac8f40>, _nodes={<DirectNode(node=<Node(_Node__handle=None, _context=<...>, _parameters={'use_sim_time': <Parameter(_type_=<Type(_value_=1, _name_='BOOL', __objclass__=<EnumMeta(_generate_next_value_=<function at remote 0x7ffff6ae9360>, __module__='rclpy.parameter', from_parameter_value=<classmethod at remote 0x7ffff673d7e0>, check=<function at remote 0x7ffff664ce50>, __doc__='An enumeration.', _member_names_=['NOT_SET', 'BOOL', 'INTEGER', 'DOUBLE', 'STRING', 'BYTE_ARRAY', 'BOOL_ARRAY', 'INTEGER_ARRAY', 'DOUBLE_ARRAY', 'STRING_ARRAY'], _member_map_={'NOT_SET': <Type...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#63 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff57aa960,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#64 _PyFunction_Vectorcall (func=<function at remote 0x7ffff57aa950>, stack=<optimized out>, nargsf=<optimized out>,
    kwnames=<optimized out>) at ../Objects/call.c:342
#65 0x00005555556c9ae8 in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db4d28,
--Type <RET> for more, q to quit, c to continue without paging--
    callable=<function at remote 0x7ffff57aa950>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#66 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db4d28,
    callable=<function at remote 0x7ffff57aa950>) at ../Include/cpython/abstract.h:123
#67 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffc770,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#68 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4198
#69 0x00005555556dfaec in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7fffe4db4b80, for file /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/executors.py, line 303, in spin_until_future_complete (future=<Future(_done=False, _cancelled=False, _result=None, _exception=None, _exception_fetched=False, _callbacks=[<method at remote 0x7ffff667f900>, <function at remote 0x7fffe4da8700>], _lock=<_thread.lock at remote 0x7ffff6c44180>, _executor=<function at remote 0x7ffff664f0a0>) at remote 0x7ffff66304f0>, timeout_sec=None), tstate=0x555555b63240)
    at ../Include/internal/pycore_ceval.h:46
#70 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff57a9d00,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#71 _PyFunction_Vectorcall (func=<function at remote 0x7ffff57a9cf0>, stack=<optimized out>, nargsf=<optimized out>,
    kwnames=<optimized out>) at ../Objects/call.c:342
#72 0x00005555556c9ae8 in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4dc8990,
    callable=<function at remote 0x7ffff57a9cf0>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#73 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4dc8990,
    callable=<function at remote 0x7ffff57a9cf0>) at ../Include/cpython/abstract.h:123
#74 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffc950,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#75 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4198
#76 0x00005555556dfaec in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7fffe4dc8800, for file /opt/ros/humble/local/lib/python3.10/dist-packages/rclpy/__init__.py, line 253, in spin_until_future_complete (node=<DirectNode(node=<Node(_Node__handle=None, _context=<Context(_lock=<_thread.lock at remote 0x7ffff3975dc0>, _callbacks=[<WeakMethod at remote 0x7fffe4d347b0>, <function at remote 0x7ffff397aa70>], _logging_initialized=True, _Context__context=<rclpy._rclpy_pybind11.Context at remote 0x7ffff3975cf0>) at remote 0x7ffff3ac8f40>, _parameters={'use_sim_time': <Parameter(_type_=<Type(_value_=1, _name_='BOOL', __objclass__=<EnumMeta(_generate_next_value_=<function at remote 0x7ffff6ae9--Type <RET> for more, q to quit, c to continue without paging--
360>, __module__='rclpy.parameter', from_parameter_value=<classmethod at remote 0x7ffff673d7e0>, check=<function at remote 0x7ffff664ce50>, __doc__='An enumeration.', _member_names_=['NOT_SET', 'BOOL', 'INTEGER', 'DOUBLE', 'STRING', 'BYTE_ARRAY', 'BOOL_ARRAY', 'INTEGER_ARRAY', 'DOUBLE_ARRAY', 'STRING_ARRAY'], _member_map_={'NOT_SET': <Type(_value_=0, _name_='NOT_SET', __objclass__=<...>) at r...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#77 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff66a0050,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#78 _PyFunction_Vectorcall (func=<function at remote 0x7ffff66a0040>, stack=<optimized out>, nargsf=<optimized out>,
    kwnames=<optimized out>) at ../Objects/call.c:342
#79 0x00005555556ceb7a in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x55555637f5f8,
    callable=<function at remote 0x7ffff66a0040>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#80 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x55555637f5f8,
    callable=<function at remote 0x7ffff66a0040>) at ../Include/cpython/abstract.h:123
#81 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffcb30,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#82 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4181
#83 0x00005555556dfaec in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x55555637f420, for file /opt/ros/humble/lib/python3.10/site-packages/ros2lifecycle/api/__init__.py, line 115, in _call_get_transitions (node=<DirectNode(node=<Node(_Node__handle=None, _context=<Context(_lock=<_thread.lock at remote 0x7ffff3975dc0>, _callbacks=[<WeakMethod at remote 0x7fffe4d347b0>, <function at remote 0x7ffff397aa70>], _logging_initialized=True, _Context__context=<rclpy._rclpy_pybind11.Context at remote 0x7ffff3975cf0>) at remote 0x7ffff3ac8f40>, _parameters={'use_sim_time': <Parameter(_type_=<Type(_value_=1, _name_='BOOL', __objclass__=<EnumMeta(_generate_next_value_=<function at remote 0x7ffff6ae9360>, __module__='rclpy.parameter', from_parameter_value=<classmethod at remote 0x7ffff673d7e0>, check=<function at remote 0x7ffff664ce50>, __doc__='An enumeration.', _member_names_=['NOT_SET', 'BOOL', 'INTEGER', 'DOUBLE', 'STRING', 'BYTE_ARRAY', 'BOOL_ARRAY', 'INTEGER_ARRAY', 'DOUBLE_ARRAY', 'STRING_ARRAY'], _member_map_={'NOT_SET': <Type(_value_=0, _name_='NOT_SET', __objclass__=<...>) at ...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#84 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff39630b0,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#85 _PyFunction_Vectorcall (func=<function at remote 0x7ffff39630a0>, stack=<optimized out>, nargsf=<optimized out>,
    kwnames=<optimized out>) at ../Objects/call.c:342
--Type <RET> for more, q to quit, c to continue without paging--
#86 0x00005555556c99a2 in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db0d88,
    callable=<function at remote 0x7ffff39630a0>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#87 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7fffe4db0d88,
    callable=<function at remote 0x7ffff39630a0>) at ../Include/cpython/abstract.h:123
#88 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffcd10,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#89 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4213
#90 0x00005555556dfaec in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7fffe4db0c10, for file /opt/ros/humble/lib/python3.10/site-packages/ros2lifecycle/api/__init__.py, line 84, in call_get_available_transitions (node=<DirectNode(node=<Node(_Node__handle=None, _context=<Context(_lock=<_thread.lock at remote 0x7ffff3975dc0>, _callbacks=[<WeakMethod at remote 0x7fffe4d347b0>, <function at remote 0x7ffff397aa70>], _logging_initialized=True, _Context__context=<rclpy._rclpy_pybind11.Context at remote 0x7ffff3975cf0>) at remote 0x7ffff3ac8f40>, _parameters={'use_sim_time': <Parameter(_type_=<Type(_value_=1, _name_='BOOL', __objclass__=<EnumMeta(_generate_next_value_=<function at remote 0x7ffff6ae9360>, __module__='rclpy.parameter', from_parameter_value=<classmethod at remote 0x7ffff673d7e0>, check=<function at remote 0x7ffff664ce50>, __doc__='An enumeration.', _member_names_=['NOT_SET', 'BOOL', 'INTEGER', 'DOUBLE', 'STRING', 'BYTE_ARRAY', 'BOOL_ARRAY', 'INTEGER_ARRAY', 'DOUBLE_ARRAY', 'STRING_ARRAY'], _member_map_={'NOT_SET': <Type(_value_=0, _name_='NOT_SET', __objclass__=<....(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#91 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff3962f90,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#92 _PyFunction_Vectorcall (func=<function at remote 0x7ffff3962f80>, stack=<optimized out>, nargsf=<optimized out>,
    kwnames=<optimized out>) at ../Objects/call.c:342
#93 0x00005555556cacf2 in _PyObject_VectorcallTstate (kwnames=('node', 'states'), nargsf=<optimized out>,
    args=<optimized out>, callable=<function at remote 0x7ffff3962f80>, tstate=0x555555b63240)
    at ../Include/cpython/abstract.h:114
#94 PyObject_Vectorcall (kwnames=('node', 'states'), nargsf=<optimized out>, args=<optimized out>,
    callable=<function at remote 0x7ffff3962f80>) at ../Include/cpython/abstract.h:123
#95 call_function (kwnames=('node', 'states'), oparg=<optimized out>, pp_stack=<synthetic pointer>,
    trace_info=0x7fffffffcef0, tstate=<optimized out>) at ../Python/ceval.c:5893
#96 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4231
--Type <RET> for more, q to quit, c to continue without paging--
#97 0x00005555556ecbe1 in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x555555ea82b0, for file /opt/ros/humble/lib/python3.10/site-packages/ros2lifecycle/verb/set.py, line 55, in main (self=<SetVerb(NAME='set') at remote 0x7ffff680eb60>, args=<Namespace(use_python_default_buffering=False,  command='lifecycle',  verb='set', _command=<LifecycleCommand(NAME='lifecycle', _subparser=<ArgumentParser(description='Various lifecycle related sub-commands', argument_default=None, prefix_chars='-', conflict_handler='error', _registries={'action': {None: <type at remote 0x555555d06670>, 'store': <type at remote 0x555555d06670>, 'store_const': <type at remote 0x555555d06a30>, 'store_true': <type at remote 0x555555d06df0>, 'store_false': <type at remote 0x555555d071b0>, 'append': <type at remote 0x555555d07570>, 'append_const': <type at remote 0x555555d07930>, 'count': <type at remote 0x555555d07cf0>, 'help': <type at remote 0x555555d080b0>, 'version': <type at remote 0x555555d08470>, 'parsers': <type at remote 0x555555d090e0>, 'extend': <type at remote 0x555555d094a0>}, 'type': {None: ...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#98 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=0x7ffff565c980, locals=0x0, con=0x7ffff3963260,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#99 _PyFunction_Vectorcall (kwnames=<optimized out>, nargsf=<optimized out>, stack=0x7ffff565c980,
    func=<function at remote 0x7ffff3963250>) at ../Objects/call.c:342
#100 _PyObject_VectorcallTstate (kwnames=<optimized out>, nargsf=<optimized out>, args=0x7ffff565c980,
    callable=<function at remote 0x7ffff3963250>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#101 method_vectorcall (method=<optimized out>, args=0x7ffff565c988, nargsf=<optimized out>, kwnames=<optimized out>)
    at ../Objects/classobject.c:53
#102 0x00005555556cacf2 in _PyObject_VectorcallTstate (kwnames=('args',), nargsf=<optimized out>, args=<optimized out>,
    callable=<method at remote 0x7ffff3957f40>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#103 PyObject_Vectorcall (kwnames=('args',), nargsf=<optimized out>, args=<optimized out>,
    callable=<method at remote 0x7ffff3957f40>) at ../Include/cpython/abstract.h:123
#104 call_function (kwnames=('args',), oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffd130,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#105 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4231
#106 0x00005555556ecbe1 in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7ffff565c800, for file /opt/ros/humble/lib/python3.10/site-packages/ros2lifecycle/command/lifecycle.py, line 38, in main (self=<LifecycleCommand(NAME='lifecycle', _subparser=<ArgumentParser(description='Various lifecycle related sub-commands', argument_default=None, prefix_chars='-', conflict_handler='error', _registries={'action': {None: <type at remote 0x555555d0--Type <RET> for more, q to quit, c to continue without paging--
6670>, 'store': <type at remote 0x555555d06670>, 'store_const': <type at remote 0x555555d06a30>, 'store_true': <type at remote 0x555555d06df0>, 'store_false': <type at remote 0x555555d071b0>, 'append': <type at remote 0x555555d07570>, 'append_const': <type at remote 0x555555d07930>, 'count': <type at remote 0x555555d07cf0>, 'help': <type at remote 0x555555d080b0>, 'version': <type at remote 0x555555d08470>, 'parsers': <type at remote 0x555555d090e0>, 'extend': <type at remote 0x555555d094a0>}, 'type': {None: <function at remote 0x7ffff5801f30>}}, _actions=[<_HelpAction(option_strings=['-h', '--help'], dest='help', nargs=0, const=None, defaul...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#107 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=0x555555ddfbf0, locals=0x0, con=0x7ffff58035c0,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#108 _PyFunction_Vectorcall (kwnames=<optimized out>, nargsf=<optimized out>, stack=0x555555ddfbf0,
    func=<function at remote 0x7ffff58035b0>) at ../Objects/call.c:342
#109 _PyObject_VectorcallTstate (kwnames=<optimized out>, nargsf=<optimized out>, args=0x555555ddfbf0,
    callable=<function at remote 0x7ffff58035b0>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#110 method_vectorcall (method=<optimized out>, args=0x555555ddfbf8, nargsf=<optimized out>, kwnames=<optimized out>)
    at ../Objects/classobject.c:53
#111 0x00005555556cacf2 in _PyObject_VectorcallTstate (kwnames=('parser', 'args'), nargsf=<optimized out>,
    args=<optimized out>, callable=<method at remote 0x7ffff57e0b00>, tstate=0x555555b63240)
    at ../Include/cpython/abstract.h:114
#112 PyObject_Vectorcall (kwnames=('parser', 'args'), nargsf=<optimized out>, args=<optimized out>,
    callable=<method at remote 0x7ffff57e0b00>) at ../Include/cpython/abstract.h:123
#113 call_function (kwnames=('parser', 'args'), oparg=<optimized out>, pp_stack=<synthetic pointer>,
    trace_info=0x7fffffffd370, tstate=<optimized out>) at ../Python/ceval.c:5893
#114 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4231
#115 0x00005555556dfaec in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x555555ddfa40, for file /opt/ros/humble/lib/python3.10/site-packages/ros2cli/cli.py, line 91, in main (script_name='ros2', argv=None, description='ros2 is an extensible command-line tool for ROS 2.', extension=<LifecycleCommand(NAME='lifecycle', _subparser=<ArgumentParser(description='Various lifecycle related sub-commands', argument_default=None, prefix_chars='-', conflict_handler='error', _registries={'action': {None: <type at remote 0x555555d06670>, 'store': <type at remote 0x555555d06670>, 'store_const': <type at remote 0x555555d06a30>, 'store_true': <type at remote 0x555555d06df0>, 'store_false': <type at remote 0x555555d071b0>, 'append': <type at remote 0x555555d07570>, 'append_const': <type at remote 0x555555d07930>, 'count': <type --Type <RET> for more, q to quit, c to continue without paging--
at remote 0x555555d07cf0>, 'help': <type at remote 0x555555d080b0>, 'version': <type at remote 0x555555d08470>, 'parsers': <type at remote 0x555555d090e0>, 'extend': <type at remote 0x555555d094a0>}, 'type': {None: <function at remote 0x7ffff5801f30>}}, _actions=[<_He...(truncated), tstate=0x555555b63240) at ../Include/internal/pycore_ceval.h:46
#116 _PyEval_Vector (kwnames=<optimized out>, argcount=<optimized out>, args=<optimized out>, locals=0x0, con=0x7ffff68e8710,
    tstate=0x555555b63240) at ../Python/ceval.c:5067
#117 _PyFunction_Vectorcall (func=<function at remote 0x7ffff68e8700>, stack=<optimized out>, nargsf=<optimized out>,
    kwnames=<optimized out>) at ../Objects/call.c:342
#118 0x00005555556c99a2 in _PyObject_VectorcallTstate (kwnames=0x0, nargsf=<optimized out>, args=0x7ffff6d29db8,
    callable=<function at remote 0x7ffff68e8700>, tstate=0x555555b63240) at ../Include/cpython/abstract.h:114
#119 PyObject_Vectorcall (kwnames=0x0, nargsf=<optimized out>, args=0x7ffff6d29db8,
    callable=<function at remote 0x7ffff68e8700>) at ../Include/cpython/abstract.h:123
#120 call_function (kwnames=0x0, oparg=<optimized out>, pp_stack=<synthetic pointer>, trace_info=0x7fffffffd550,
    tstate=<optimized out>) at ../Python/ceval.c:5893
#121 _PyEval_EvalFrameDefault (tstate=<optimized out>, f=<optimized out>, throwflag=<optimized out>) at ../Python/ceval.c:4213
#122 0x00005555557aee56 in _PyEval_EvalFrame (throwflag=0,
    f=Frame 0x7ffff6d29c40, for file /opt/ros/humble/bin/ros2, line 33, in <module> (), tstate=0x555555b63240)
    at ../Include/internal/pycore_ceval.h:46
#123 _PyEval_Vector (tstate=0x555555b63240, con=<optimized out>, locals=<optimized out>, args=<optimized out>,
    argcount=<optimized out>, kwnames=<optimized out>) at ../Python/ceval.c:5067
#124 0x00005555557aed26 in PyEval_EvalCode (co=<code at remote 0x7ffff6cacbe0>,
    globals={'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <SourceFileLoader(name='__main__', path='/opt/ros/humble/bin/ros2') at remote 0x7ffff6be18d0>, '__spec__': None, '__annotations__': {}, '__builtins__': <module at remote 0x7ffff6d94950>, '__file__': '/opt/ros/humble/bin/ros2', '__cached__': None, 're': <module at remote 0x7ffff6ad0ea0>, 'sys': <module at remote 0x7ffff6d82390>, '__requires__': 'ros2cli==0.18.11', 'distribution': <function at remote 0x7ffff6afdea0>, 'importlib_load_entry_point': <function at remote 0x7ffff6d63d90>, 'load_entry_point': <function at remote 0x7ffff6d63d90>},
    locals=<optimized out>) at ../Python/ceval.c:1134
#125 0x00005555557d5ae8 in run_eval_code_obj (tstate=0x555555b63240, co=0x7ffff6cacbe0,
    globals={'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <SourceFileLoader(name='__main__', path='/opt/ros/humble/bin/ros2') at remote 0x7ffff6be18d0>, '__spec__': None, '__annotations__': {}, '__builtins__': <module at re--Type <RET> for more, q to quit, c to continue without paging--
mote 0x7ffff6d94950>, '__file__': '/opt/ros/humble/bin/ros2', '__cached__': None, 're': <module at remote 0x7ffff6ad0ea0>, 'sys': <module at remote 0x7ffff6d82390>, '__requires__': 'ros2cli==0.18.11', 'distribution': <function at remote 0x7ffff6afdea0>, 'importlib_load_entry_point': <function at remote 0x7ffff6d63d90>, 'load_entry_point': <function at remote 0x7ffff6d63d90>},
    locals={'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <SourceFileLoader(name='__main__', path='/opt/ros/humble/bin/ros2') at remote 0x7ffff6be18d0>, '__spec__': None, '__annotations__': {}, '__builtins__': <module at remote 0x7ffff6d94950>, '__file__': '/opt/ros/humble/bin/ros2', '__cached__': None, 're': <module at remote 0x7ffff6ad0ea0>, 'sys': <module at remote 0x7ffff6d82390>, '__requires__': 'ros2cli==0.18.11', 'distribution': <function at remote 0x7ffff6afdea0>, 'importlib_load_entry_point': <function at remote 0x7ffff6d63d90>, 'load_entry_point': <function at remote 0x7ffff6d63d90>})
    at ../Python/pythonrun.c:1291
#126 0x00005555557d02ef in run_mod (mod=<optimized out>, filename=<optimized out>,
    globals={'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <SourceFileLoader(name='__main__', path='/opt/ros/humble/bin/ros2') at remote 0x7ffff6be18d0>, '__spec__': None, '__annotations__': {}, '__builtins__': <module at remote 0x7ffff6d94950>, '__file__': '/opt/ros/humble/bin/ros2', '__cached__': None, 're': <module at remote 0x7ffff6ad0ea0>, 'sys': <module at remote 0x7ffff6d82390>, '__requires__': 'ros2cli==0.18.11', 'distribution': <function at remote 0x7ffff6afdea0>, 'importlib_load_entry_point': <function at remote 0x7ffff6d63d90>, 'load_entry_point': <function at remote 0x7ffff6d63d90>},
    locals={'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <SourceFileLoader(name='__main__', path='/opt/ros/humble/bin/ros2') at remote 0x7ffff6be18d0>, '__spec__': None, '__annotations__': {}, '__builtins__': <module at remote 0x7ffff6d94950>, '__file__': '/opt/ros/humble/bin/ros2', '__cached__': None, 're': <module at remote 0x7ffff6ad0ea0>, 'sys': <module at remote 0x7ffff6d82390>, '__requires__': 'ros2cli==0.18.11', 'distribution': <function at remote 0x7ffff6afdea0>, 'importlib_load_entry_point': <function at remote 0x7ffff6d63d90>, 'load_entry_point': <function at remote 0x7ffff6d63d90>},
    flags=<optimized out>, arena=<optimized out>) at ../Python/pythonrun.c:1312
#127 0x00005555557d5885 in pyrun_file (fp=fp@entry=0x555555ba79b0, filename=filename@entry='/opt/ros/humble/bin/ros2',
    start=start@entry=257,
    globals=globals@entry={'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <SourceFileLoader(name='__main__', path='/opt/ros/humble/bin/ros2') at remote 0x7ffff6be18d0>, '__spec__': None, '__annotations__': {}, '__builtins__': <module at remote 0x7ffff6d94950>, '__file__': '/opt/ros/humble/bin/ros2', '__cached__': None, 're': <module at remote 0x7ffff6ad0ea0>, 'sys': <module at remote 0x7ffff6d82390>, '__requires__': 'ros2cli==0.18.11', 'distribution': <function at remote 0x7ffff6afdea0>, 'importlib_load_entry_point': <function at remote 0x7ffff6d63d90>, 'load_entry_point': <function at remote 0x7ffff6d63d90>},
--Type <RET> for more, q to quit, c to continue without paging--
    locals=locals@entry={'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <SourceFileLoader(name='__main__', path='/opt/ros/humble/bin/ros2') at remote 0x7ffff6be18d0>, '__spec__': None, '__annotations__': {}, '__builtins__': <module at remote 0x7ffff6d94950>, '__file__': '/opt/ros/humble/bin/ros2', '__cached__': None, 're': <module at remote 0x7ffff6ad0ea0>, 'sys': <module at remote 0x7ffff6d82390>, '__requires__': 'ros2cli==0.18.11', 'distribution': <function at remote 0x7ffff6afdea0>, 'importlib_load_entry_point': <function at remote 0x7ffff6d63d90>, 'load_entry_point': <function at remote 0x7ffff6d63d90>}, closeit=closeit@entry=1, flags=0x7fffffffd7f8) at ../Python/pythonrun.c:1208
#128 0x00005555557d4e68 in _PyRun_SimpleFileObject (fp=0x555555ba79b0, filename='/opt/ros/humble/bin/ros2', closeit=1,
    flags=0x7fffffffd7f8) at ../Python/pythonrun.c:456
#129 0x00005555557d4b47 in _PyRun_AnyFileObject (fp=0x555555ba79b0, filename='/opt/ros/humble/bin/ros2', closeit=1,
    flags=0x7fffffffd7f8) at ../Python/pythonrun.c:90
#130 0x00005555557c902e in pymain_run_file_obj (skip_source_first_line=0, filename='/opt/ros/humble/bin/ros2',
    program_name='/usr/bin/python3') at ../Modules/main.c:353
#131 pymain_run_file (config=0x555555b474c0) at ../Modules/main.c:372
#132 pymain_run_python (exitcode=0x7fffffffd7f4) at ../Modules/main.c:587
#133 Py_RunMain () at ../Modules/main.c:666
#134 0x00005555557a2d6d in Py_BytesMain (argc=<optimized out>, argv=<optimized out>) at ../Modules/main.c:720
#135 0x00007ffff7c29d90 in __libc_start_call_main (main=main@entry=0x5555557a2d30 <main>, argc=argc@entry=6,
    argv=argv@entry=0x7fffffffda08) at ../sysdeps/nptl/libc_start_call_main.h:58
#136 0x00007ffff7c29e40 in __libc_start_main_impl (main=0x5555557a2d30 <main>, argc=6, argv=0x7fffffffda08,
    init=<optimized out>, fini=<optimized out>, rtld_fini=<optimized out>, stack_end=0x7fffffffd9f8)
    at ../csu/libc-start.c:392
#137 0x00005555557a2c65 in _start ()
```
